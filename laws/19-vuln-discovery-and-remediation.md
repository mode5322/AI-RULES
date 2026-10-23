# 19 — Vulnerability Discovery and Remediation

## Purpose

Define the **authorized** vulnerability **discovery → triage → remediation closure plan → fix gate** workflow for the Security Laws suite. This module sits under the parent policy in `10-security.md` and consumes discovery outputs from `18-security-tooling.md` — including basic scanners **and** the vendored multi-phase skill at `.cursor/skills/security-audit/` (Cloudflare `security-audit-skill`). It turns findings into structured **Remediation Closure Prompt/Plans**, waits for user choice (`15-error-handling.md`), then validates fixes against architecture, DB, logic, validation, change-management, quality, and final-verification laws.

Discovery may include sandboxed validation and reproduction evidence produced by the `security-audit` skill. Remediation code changes still require the fix gate below.

## Security Laws suite (must-follow when security applies)

| Role | Module | Responsibility |
|---|---|---|
| **Parent — policy / review** | `10-security.md` | Secrets, authz, input safety, least privilege; owns the suite |
| **Companion — tools + audit skill** | `18-security-tooling.md` | Optional scanners (deps, secrets, Semgrep, ZAP baseline, platform checklists) + `.cursor/skills/security-audit/` |
| **Companion — discover → close** | `19-vuln-discovery-and-remediation.md` (this file) | Authorized discovery intake, triage, remediation plans, fix gate, post-fix validation |

Reading order when security work applies: **`10` → `18` (if tooling enabled) → `19` (when findings or vuln closure is in scope).**

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`



## When this module applies / when to skip

- Applies when: tooling or the `security-audit` skill (`18`) produces findings; `10` / `13` / `16` review identifies vulnerabilities; the user requests a security discovery or remediation pass; or PROFILE enables this module.
- Applies on new-project security baselines and existing-project audits — depth scales with risk and user choice.
- Skip a discovery run unless the user asked for it. Also skip when the user declined discovery for this session, there is no code or secret surface, or the scope is docs only. Still honor the lightweight review in `10`.
- MUST NOT skip the fix-gate / wait-for-user rule when remediating any confirmed finding.
- Cross-links (mandatory awareness):
  - Suite parent / tools → `10-security.md`, `18-security-tooling.md`
  - Must not break other components → `05-architecture.md`
  - Data / schema impact → `06-database.md`
  - Calculation / business-rule correctness → `07-logic-and-math.md`
  - Input contracts after fixes → `08-validation.md`
  - Scope and rollout of remediations → `11-change-management.md`
  - Structure and readability of fixes → `12-code-quality.md`
  - Done criteria → `14-final-verification.md`
  - Present findings and wait before code change → `15-error-handling.md`
  - Audit framing on built repos → `16-existing-projects.md`

## Hard rules (MUST / MUST NOT)

### Authorized targets only

- MUST discover only on **authorized** targets: this user’s project, localhost, staging, or targets the user **explicitly confirmed**.
- MUST prefer localhost / staging over production; MUST get explicit confirmation before any non-local URL or host.
- MUST NOT scan or probe unauthorized third-party systems, random internet hosts, or production without explicit written confirmation in the session.

### Discovery sources (`18` tracks A and B)

- MUST discover via `10-security.md` review **plus** enabled tools from `18-security-tooling.md`:
  - Track **A**: dependency auditors, secret scanners (`gitleaks` / `trufflehog`), light SAST (`semgrep`), OWASP ZAP **baseline** (confirmed web targets), platform checklists.
  - Track **B**: `.cursor/skills/security-audit/` when the user asks for a security audit, pen-test-style review, or report artifacts. Follow that skill’s workflow and keep its validators (`validate-findings.cjs`, `validate-coverage-ledger.cjs`).
- Track **B** is an approved pack path. MUST NOT treat it as an unauthorized duplicate of track **A**.
- **Nuclei** (and similar): enable only when the user explicitly asks, limited to confirmed localhost or staging.
- MUST NOT treat green scans as “secure” without completing `10` policy review.

### Mapping `security-audit` records into this module

When track **B** produces `findings.json`:

- `confirmed` → actionable finding for triage + Remediation Closure Plan.
- `needs_validation` → present as unresolved; do not invent severity; keep the skill’s unresolved fact; may still offer a Closure Plan that focuses on how to validate or harden.
- `rejected` → record as disproved; do not remediate as a vulnerability.

Evidence, reproduction notes, and validator output from the skill MAY be carried into the Closure Plan. Fixing code still waits for user choice.

### Closure gate (not silent fix)

- MUST NOT silently “fix all” findings or auto-apply remediations without user choice.
- MUST NOT expand ZAP beyond baseline in track **A** unless the user asks for a deeper mode.
- MUST NOT add Nuclei as a required default tool.

### Triage

- MUST triage each actionable finding (or coherent finding theme) as **critical / medium / low** (for `needs_validation`, severity may remain unset until confirmed).
- MUST add an exploitability / reachability note (e.g. “reachable without auth,” “requires admin,” “needs local file access”), including validation evidence from track **B** when present.
- MUST flag likely false positives for user confirmation when ambiguous.
- MUST prefer grouping duplicate/same-root-cause findings into one remediation plan when appropriate.

### Remediation Closure Prompt / Plan (per finding or theme)

Before any code change, MUST generate a **Remediation Closure Prompt/Plan** that includes all of:

1. **What / where / why it matters** — concise finding statement, location (file/package/URL area), business/security impact
2. **Root cause hypothesis** — structural cause, not only the symptom line
3. **4 fix options + option 5 custom blank + exactly one Recommended** (same shape as `15-error-handling.md` / question protocol)
4. **Side-effect / compatibility impact** — architecture (`05`), database (`06`), UI/other modules, shared services
5. **Quick fix vs root-cause rule** — quick fix may be Recommended **only** if impact is isolated and **no** project-wide impact; otherwise Recommend root-cause that preserves compatibility (`16`)
6. **Post-fix verification checklist** — what to re-check after the chosen fix (suite + validation hooks below)

### Fix gate

- MUST **wait for the user’s choice** before any remediation code change (`15-error-handling.md`).
- MUST apply only the chosen option (or clarified follow-up if still ambiguous).
- After the fix: MUST run applicable validation hooks from `08`, `05`, `06`, `07`, `11`, `12`, `14`, plus the five-point post-change review in `00-core.md`.

## Remediation Closure Prompt template

```markdown
### Finding
Severity: critical | medium | low
What: <concise vulnerability / weakness>
Where: <file / package / surface>
Why it matters: <impact>
Exploitability / evidence: <reachability + optional validation notes from security-audit skill>

### Root cause hypothesis
<root cause — structural if applicable>

### Remediation options
1. <option A>
2. <option B> — **Recommended**
3. <option C>
4. <option D>
5. Other: _______________

### Compatibility / side effects
- Architecture (`05`): <none | …>
- Database (`06`): <none | …>
- Logic / math (`07`): <none | …>
- Validation (`08`): <none | …>
- UI / other modules: <none | …>
- Change scope (`11`): <isolated | shared | cross-cutting>

### Quick vs root-cause
Quick fix allowed as Recommended only if no project-wide impact: yes | no — <reason>

### Post-fix verification checklist
- [ ] Re-check finding class (tooling `18` and/or `10` review)
- [ ] Architecture compatibility (`05`)
- [ ] DB compatibility if touched (`06`)
- [ ] Logic/math if touched (`07`)
- [ ] Validation / contracts (`08`)
- [ ] Change-management notes (`11`)
- [ ] Code quality / structure (`12`)
- [ ] Final verification hooks (`14`)
- [ ] Five-point review (`00-core`)

Hints:
- Recommended because: <root-cause / safety / compatibility>
- Trade-off: <speed vs durability>
```

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Complete `10-security.md` decisions (auth, secrets, roles) first.
2. Optionally enable `18-security-tooling.md` via question protocol; record PROFILE.
3. Ask whether to enable this module (`19`); confirm authorized targets.
4. **Discovery:** run `10` review + approved `18` tools (track A and/or track B).
5. **Triage:** severity + exploitability/evidence notes; map `findings.json` verdicts when track B ran; dedupe themes.
6. **Remediation plans:** one Closure Prompt/Plan per finding or theme; wait for user choice (`15`).
7. **Fix** only the chosen options; prefer root-cause when impact is structural.
8. **Validate** with hooks from `08`, `05`, `06`, `07`, `11`, `12`, `14` as applicable + five-point review.
9. Do not add a settings blank for findings. Report them in the reply and wait before fixing.

## Existing-project workflow

1. Frame under `16-existing-projects.md` / `13-ai-review.md` — do not “patch first.”
2. Confirm authorized targets and whether `18` tooling is in scope (full-repo baseline often **Recommended** on first AI security onboarding).
3. Discovery via `10` + `18` (A and/or B) → triage → issue/fix plan that includes Remediation Closure Plans.
4. Structural secret/authz/injection patterns → Recommend root-cause with compatibility notes (`05`, `06`, `11`).
5. Wait for user choice per finding/theme before code changes (`15`).
6. After fixes, re-run relevant scanners/checklists and `14-final-verification.md`.
7. Update PROFILE with residual accepted risks (only when user explicitly accepts).

## Workflow summary

1. **Discovery** — `18` track A and/or B (when enabled) + `10` review on authorized targets only  
2. **Triage** — critical / medium / low + exploitability/evidence (map skill verdicts when present)  
3. **Remediation Closure Prompt/Plan** — what/where/why, root cause, 4+custom options, side effects, quick vs root-cause, verification checklist  
4. **Wait** — user chooses before any code change (`15`)  
5. **Fix + validate** — apply choice; run `08` / `05` / `06` / `07` / `11` / `12` / `14` hooks as applicable  

## Post-change checklist hooks

- [ ] Target authorization confirmed before discovery
- [ ] Discovery used `10` + `18` (track A and/or B); Nuclei not treated as required by default
- [ ] Track B followed `.cursor/skills/security-audit/` when a full audit was requested
- [ ] Findings triaged (severity + exploitability/evidence); skill verdicts mapped when present
- [ ] Remediation Closure Plan generated before code changes
- [ ] User choice recorded; fix gate honored (`15`)
- [ ] Compatibility checked (`05`, `06`, UI/other modules as needed)
- [ ] Validation / logic / change-management / quality hooks run as applicable (`08`, `07`, `11`, `12`)
- [ ] Final verification (`14`) + five-point review (`00-core`)
- [ ] No discovery ran unless the user asked for it

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
