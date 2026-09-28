# 19 — Vulnerability Discovery and Remediation

## Purpose

Define the **authorized** vulnerability **discovery → triage → remediation closure plan → fix gate** workflow for the Security Laws suite. This module sits under the parent policy in `10-security.md` and consumes defensive scan outputs from `18-security-tooling.md`. It turns findings into structured **Remediation Closure Prompt/Plans**, waits for user choice (`15-error-handling.md`), then validates fixes against architecture, DB, logic, validation, change-management, quality, and final-verification laws.

**Discovery ≠ exploitation.** This module never authorizes writing exploits, attack PoCs, or offensive playbooks.

## Security Laws suite (must-follow when security applies)

| Role | Module | Responsibility |
|---|---|---|
| **Parent — policy / review** | `10-security.md` | Secrets, authz, input safety, least privilege; owns the suite |
| **Companion — defensive tools** | `18-security-tooling.md` | Optional stack-adaptive scanners (deps, secrets, Semgrep, ZAP baseline, platform checklists) |
| **Companion — discover → close** | `19-vuln-discovery-and-remediation.md` (this file) | Authorized discovery intake, triage, remediation plans, fix gate, post-fix validation |

Reading order when security work applies: **`10` → `18` (if tooling enabled) → `19` (when findings or vuln closure is in scope).**

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`

Current: _______________

If `N/A`, reason: _______________

## When this module applies / when to skip

- Applies when: defensive tooling (`18`) produces findings; `10` / `13` / `16` review identifies vulnerabilities; the user requests a security discovery or remediation pass; or PROFILE enables this module.
- Applies on new-project security baselines and existing-project audits — depth scales with risk and user choice.
- Skip full discovery runs when: module is `N/A` after questioning; user declined discovery for this session; no code/deps/secrets/web surface; or pure docs with no executable impact (still honor `10` lightweight review).
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

### Discovery sources (prefer `18` basic set)

- MUST prefer discovery via `10-security.md` review **plus** enabled tools from `18-security-tooling.md`: dependency auditors, secret scanners (`gitleaks` / `trufflehog`), light SAST (`semgrep`), OWASP ZAP **baseline** (confirmed web targets), and platform checklists.
- MUST NOT invent a parallel scanner stack that duplicates `18` without PROFILE justification.
- **Nuclei** (and similar aggressive template-driven scanners): **not in the basic set**. Enable only if PROJECT-SPECIFIC explicitly opts in **and** the user re-approves via question protocol, limited to confirmed localhost/staging. Origin template stays basic-set (`18`) only.
- MUST NOT treat green scans as “secure” without completing `10` policy review.

### FORBIDDEN — state and enforce

- MUST NOT write exploits, weaponized payloads, attack PoCs, Metasploit modules, or offensive step-by-step intrusion playbooks — including for “authorized labs,” CTFs framed as the product, or localhost.
- MUST NOT equate discovery with exploitation: report **what** was found and **why it matters** at a high level; do not demonstrate compromise.
- MUST NOT expand ZAP beyond baseline in the default pack, and MUST NOT add Nuclei as a required tool.
- MUST NOT silently “fix all” findings or auto-apply remediations without user choice.

### Triage

- MUST triage each actionable finding (or coherent finding theme) as **critical / medium / low**.
- MUST add a **high-level exploitability note** (e.g. “reachable without auth,” “requires admin,” “needs local file access”) — **without** PoC code, payloads, or reproduction attack steps.
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
Exploitability (high level, no PoC): <e.g. unauthenticated HTTP path / requires privileged role / local-only>

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

Follow `templates/question-protocol.md`. Ask **one** question at a time.

### Example — Enable discovery / remediation flow?

```markdown
### Question
Enable authorized vulnerability discovery and remediation planning for this session/project?

1. Yes — use `10` review + enabled `18` basic tools, then triage via this module — **Recommended**
2. Yes — `10` review only (no scanners this time); still use remediation plans for manual findings
3. Not now — keep policy review only; revisit on audit
4. Mark module N/A for this project (document reason)
5. Other: _______________

Hints:
- Recommended when shipping auth, payments, multi-user data, or public web surfaces.
- To decide: check PROFILE Security suite fields and whether `18` is already ACTIVE.
- Discovery stays defensive; no exploits or PoCs.
```

### Example — Confirm discovery targets

```markdown
### Question
Which targets are authorized for this discovery pass?

1. This repository + localhost only — **Recommended**
2. This repository + confirmed staging URL(s)
3. Changed areas / current task paths only (no network scan)
4. Broader scope (list exact hosts/URLs in custom — must be explicit)
5. Other: _______________

Hints:
- Recommended to avoid accidental production or third-party probing.
- MUST confirm exact non-local URLs before any network scan (`18` ZAP baseline rules still apply).
```

### Example — After triage, proceed to remediation plans?

```markdown
### Question
How should we proceed after triage?

1. Generate Remediation Closure Plans for critical + medium now — **Recommended**
2. Critical only first; defer medium/low
3. Full list including low (may be noisy)
4. Pause — user will prioritize offline
5. Other: _______________
```

## New-project workflow

1. Complete `10-security.md` decisions (auth, secrets, roles) first.
2. Optionally enable `18-security-tooling.md` via question protocol; record PROFILE.
3. Ask whether to enable this module (`19`); confirm authorized targets.
4. **Discovery:** run `10` review + approved `18` tools (basic set unless PROFILE opts into more).
5. **Triage:** severity + high-level exploitability notes (no PoCs); dedupe themes.
6. **Remediation plans:** one Closure Prompt/Plan per finding or theme; wait for user choice (`15`).
7. **Fix** only the chosen options; prefer root-cause when impact is structural.
8. **Validate** with hooks from `08`, `05`, `06`, `07`, `11`, `12`, `14` as applicable + five-point review.
9. Fill PROJECT-SPECIFIC: enablement, last discovery scope, open vs closed finding themes.

## Existing-project workflow

1. Frame under `16-existing-projects.md` / `13-ai-review.md` — do not “patch first.”
2. Confirm authorized targets and whether `18` tooling is in scope (full-repo baseline often **Recommended** on first AI security onboarding).
3. Discovery via `10` + `18` → triage → issue/fix plan that includes Remediation Closure Plans.
4. Structural secret/authz/injection patterns → Recommend root-cause with compatibility notes (`05`, `06`, `11`).
5. Wait for user choice per finding/theme before code changes (`15`).
6. After fixes, re-run relevant scanners/checklists and `14-final-verification.md`.
7. Update PROFILE with residual accepted risks (only when user explicitly accepts).

## Workflow summary

1. **Discovery** — `18` tools (when enabled) + `10` review on authorized targets only  
2. **Triage** — critical / medium / low + high-level exploitability (no PoC)  
3. **Remediation Closure Prompt/Plan** — what/where/why, root cause, 4+custom options, side effects, quick vs root-cause, verification checklist  
4. **Wait** — user chooses before any code change (`15`)  
5. **Fix + validate** — apply choice; run `08` / `05` / `06` / `07` / `11` / `12` / `14` hooks as applicable  

## Post-change checklist hooks

- [ ] Target authorization confirmed before discovery
- [ ] Discovery used `10` + `18` basic set (or documented PROFILE extras); Nuclei not treated as required
- [ ] No exploits, PoCs, or offensive procedures produced
- [ ] Findings triaged (severity + high-level exploitability)
- [ ] Remediation Closure Plan generated before code changes
- [ ] User choice recorded; fix gate honored (`15`)
- [ ] Compatibility checked (`05`, `06`, UI/other modules as needed)
- [ ] Validation / logic / change-management / quality hooks run as applicable (`08`, `07`, `11`, `12`)
- [ ] Final verification (`14`) + five-point review (`00-core`)
- [ ] PROFILE / PROJECT-SPECIFIC updated for enablement and residual risk

## PROJECT-SPECIFIC

- Status: ACTIVE | N/A | PROJECT-SPECIFIC | _______________
- Suite reading confirmed (`10` + `18` + `19`): yes | no | _______________
- Discovery enabled: yes | no | partial — _______________
- Authorized targets: repo | localhost | staging URLs: _______________ | _______________
- Default discovery sources: `10` review | `18` basic set | PROFILE extras: _______________
- Nuclei / aggressive scanners: disabled (default) | PROJECT-SPECIFIC opt-in: _______________
- Last discovery date / scope: _______________
- Open finding themes: _______________
- Closed / accepted residual risks: _______________
- N/A rationale: _______________
