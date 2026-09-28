# 18 — Security Tooling (Defensive)

## Purpose

Add an **optional, defensive tooling layer** that supplements — never replaces — the policy and AI security review in `10-security.md`. Tools adapt to detected project type / stack, including **mixed monorepos** (e.g. Flutter app + React admin + static web). Agents run scanners only after question-protocol approval (or one-time deferral per `templates/deferral.md`).

This module encodes the **basic defensive set** (no Nuclei, no Metasploit, no exploits, no attack PoCs, no offensive procedures):

1. Dependency auditors (package-manager native where available)
2. Secret scanners (`gitleaks` preferred; `trufflehog` alternate)
3. Light SAST (`semgrep` with community / OWASP-oriented configs)
4. OWASP ZAP **Baseline only** — web targets only, after scope confirmation
5. Platform rule-based checks for mobile/desktop (checklist-driven; optional native tools if already present)

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`

Current: _______________

If `N/A`, reason: _______________

## When this module applies / when to skip

- Applies when the user opts into defensive scans, when PROFILE enables tooling, or when a security review (`10`, `13`, `16`) recommends automated checks.
- Applies on new-project security setup and on existing-project audits — depth scales with risk and user choice.
- Skip running tools when: module is `N/A` after questioning; user declined tooling for this session; no installable/runnable target for a given tool; or scope is pure docs with no code/deps/secrets surface.
- MUST NOT treat tooling as a substitute for `10-security.md` review (secrets, authz, validation, least privilege).
- Cross-links: policy/review → `10-security.md`; findings presentation → `15-error-handling.md`; discovery findings MUST enter remediation → `19-vuln-discovery-and-remediation.md`; existing audits → `16-existing-projects.md` / `13-ai-review.md`; functional tests ≠ security scans → `09-testing.md`.

## Hard rules (MUST / MUST NOT)

### Defensive only

- MUST run only **defensive** scanners and checklists listed in this module (or PROJECT-SPECIFIC equivalents of the same class).
- MUST NOT write exploits, attack PoCs, Metasploit modules, offensive payloads, or unauthorized-access procedures — even for “authorized labs,” CTFs framed as the product, or localhost.
- MUST NOT expand ZAP beyond **baseline** mode in this pack’s default set.
- MUST NOT add Nuclei or other aggressive template-driven attack scanners unless the consuming project later adds an explicit PROJECT-SPECIFIC exception **and** the user re-approves via question protocol (origin template stays basic-set only).

### Gate before running

- MUST ask via `templates/question-protocol.md` before installing or running security tools, unless the user deferred **for this time only**.
- MUST confirm stacks present, scan scope (whole repo vs changed areas), and any web target URL before ZAP baseline.
- MUST prefer localhost / staging targets over production; MUST get explicit confirmation before scanning any non-local URL.
- MUST wait for user choice before acting on tool enablement or finding remediations.

### Findings → remediation + error-handling flow

- MUST route each actionable finding (or grouped finding theme) into `19-vuln-discovery-and-remediation.md`: triage → remediation plan → gate related laws → present via `15-error-handling.md` (4 fix options + **Recommended** + custom blank) → **wait** before fixing.
- MUST prefer root-cause fixes when findings indicate structural impact (systemic secret leakage, missing authz pattern, dependency class-wide failure).
- MUST NOT silently “fix all” scanner noise; triage severity and false positives with the user when ambiguous.
- After the chosen fix: run the mandatory five-point post-change review (`00-core.md`) and `19` re-verify hooks.

### Stack adaptation & mixed repos

- MUST detect package managers, lockfiles, and app roots **per area** — never assume one stack for the whole repository.
- In mixed monorepos, MUST run only the **relevant subset** of tools for each package/area (e.g. `dart pub` / Flutter checks under the Flutter app; `npm audit` under the React admin; ZAP only if a web URL is in scope).
- MUST map dependency audits to the package manager(s) found (see matrix below).
- Secrets (`gitleaks` / `trufflehog`) and light SAST (`semgrep`) generally apply wherever source code exists, subject to excluded paths.
- Platform mobile/desktop checks are **checklist-first**; invoke optional native tooling only if already installed and user-approved.

### Tooling hygiene

- MUST record enabled tools, targets, and excluded paths in PROJECT-SPECIFIC / project profile when confirmed.
- MUST NOT commit scanner credentials, API tokens for commercial scanners, or raw reports that embed secrets.
- Prefer read-only / non-destructive scan modes; do not mutate production data as part of a scan.

## Stack detection / mapping matrix

Detect by lockfiles, manifests, and folder layout. Apply the union of rows that match. Commands are **high-level names** (install/run); adapt to OS and local PATH. No exploit payloads.

| Stack / area | How to detect (examples) | Dependency audit | Secrets | Light SAST | ZAP baseline | Platform checks |
|---|---|---|---|---|---|---|
| **React / Next / Vite SPA** | `package.json` + React/Next/Vite deps; `next.config.*`, `vite.config.*` | `npm audit` / `pnpm audit` / `yarn npm audit` (match lockfile) | `gitleaks` (pref.) / `trufflehog` | `semgrep` (JS/TS + OWASP-oriented community rules) | Yes — if confirmed web URL/target | Web checklist (headers, cookies, CSP notes) via review; ZAP covers passive baseline |
| **Default web** | Static HTML/CSS/JS; generic backend+frontend without SPA framework markers | Per backend package manager if any; else skip dep audit for pure static | Same | `semgrep` on present languages; skip if no code worth scanning | Yes — if confirmed web URL/target | Same web checklist |
| **Flutter** (mobile and/or web) | `pubspec.yaml`, `lib/`, `android/` / `ios/` / `web/` | `dart pub outdated` / Flutter dependency review; use Dart/Flutter advisory workflow available in toolchain | Same (repo-wide) | `semgrep` where rules apply; plus Flutter/Dart checklist | Only if Flutter **web** (or separate web shell) has a confirmed URL | Mobile/desktop checklist (storage, deep links, cleartext, backup, permissions); optional native tools if present |
| **React Native** | `package.json` + `react-native`; `android/` / `ios/` | `npm`/`yarn`/`pnpm` audit | Same | `semgrep` JS/TS + mobile checklist | Only if a web/dev URL is explicitly in scope | Mobile checklist; optional native tools if present |
| **Node backend** | `package.json` without (or beside) UI; Express/Fastify/Nest/etc. | `npm`/`pnpm`/`yarn` audit | Same | `semgrep` JS/TS backend rules | Only if HTTP API/UI URL confirmed | API/auth checklist under `10-security.md` |
| **Python backend** | `requirements.txt`, `pyproject.toml`, `Pipfile` | `pip-audit` (or `poetry`/`pipenv` equivalent advisory flow) | Same | `semgrep` Python / OWASP-oriented | If web URL confirmed | Same API checklist |
| **PHP backend** | `composer.json` | `composer audit` | Same | `semgrep` PHP rules when available | If web URL confirmed | Same API checklist |
| **Desktop — Electron** | `package.json` + Electron | Node audit as above | Same | `semgrep` + Electron checklist (nodeIntegration, contextIsolation, shell.open) | Only if app loads remote/web URL in scope | Desktop checklist |
| **Desktop — Tauri** | `src-tauri/`, `Cargo.toml` + frontend package | Frontend PM audit + `cargo audit` if Rust deps present and approved | Same | `semgrep` on UI + Tauri/Rust checklist | If webview URL in scope | Desktop checklist |
| **Desktop — .NET** | `*.csproj`, `.sln` | `dotnet list package --vulnerable` (or equivalent) | Same | `semgrep` if C# rules available; else checklist | If hosted web UI URL in scope | Desktop checklist |
| **Mixed monorepo** | Multiple of the above | **Per package/area** — never one audit for whole repo unless single PM | Repo-wide with path excludes | Per language roots | Only areas with confirmed web targets | Per platform area |

### When to skip a tool (per stack)

| Tool | Skip when |
|---|---|
| Dependency audit | No lockfile/manifest for that area; or user excluded the package |
| Secrets | No VCS/history/files in scope; or user deferred secrets scan |
| Semgrep | No source files; unsupported languages only; or user declined SAST |
| ZAP baseline | No web URL; user refused non-local scan; target is production without explicit approval; or stack is mobile/desktop-only with no web surface |
| Platform checklist | Platform not in repo; mark items N/A with reason |

### Example high-level commands (defensive)

Illustrative only — use the project’s package manager and documented install method:

- Secrets: `gitleaks detect` (or `trufflehog filesystem` / git scan as alternate)
- SAST: `semgrep --config=auto` or project-pinned community/OWASP rulesets
- Node: `npm audit` (or `pnpm audit` / `yarn npm audit`)
- Python: `pip-audit`
- PHP: `composer audit`
- Flutter/Dart: `dart pub outdated` / Flutter tooling advisory commands available locally
- .NET: `dotnet list package --vulnerable`
- Rust (Tauri): `cargo audit` when approved
- ZAP: OWASP ZAP **baseline** scan against the **user-confirmed** target URL only

## Platform rule-based checks (mobile / desktop)

Checklist-driven; complete relevant items during review. Optional native tools (e.g. platform lint/analyzers already in the repo) may be run only if present and user-approved.

### Mobile (Flutter / React Native / similar)

- [ ] No secrets in source, assets, or build configs
- [ ] Sensitive data not stored in cleartext prefs / local stores without justification
- [ ] Transport: HTTPS / certificate expectations documented; cleartext traffic disabled unless explicitly required
- [ ] Permissions minimized; dangerous permissions justified
- [ ] Deep links / app links validated; no open intent/URL redirection without checks
- [ ] Backup / debug flags appropriate for release builds
- [ ] WebView (if any): JS bridge and URL allowlists reviewed (`10-security.md`)

### Desktop (Electron / Tauri / .NET)

- [ ] Auto-update and code-signing story understood (or marked out of scope)
- [ ] Electron: `contextIsolation` on; `nodeIntegration` off for untrusted content; navigation/shell open restricted
- [ ] Tauri / native: capability / permission allowlists least-privilege
- [ ] Local IPC / plugins do not expose raw shell without validation
- [ ] Log files do not retain secrets

## Question protocol

Follow `templates/question-protocol.md`. Ask **one** question at a time.

### Example — Enable tooling now?

```markdown
### Question
Enable the defensive security tooling layer for this session/project?

1. Yes — basic set (deps, secrets, Semgrep, ZAP baseline if web, platform checklists) — **Recommended**
2. Yes — secrets + dependency audit only (lighter)
3. Not now — keep `10-security.md` review only; revisit later
4. Mark module N/A for this project (document reason)
5. Other: _______________

Hints:
- Recommended when shipping auth, payments, multi-user data, or public web surfaces.
- To decide: check PROFILE “Security tooling” and whether CI already runs equivalent scans.
- Trade-off: fuller set finds more; needs install time and triage of false positives.
```

### Example — Which stacks are in this project?

```markdown
### Question
Which stacks / areas should security tooling cover?

1. Single primary stack already detected — use that mapping only — **Recommended** when one lockfile/root
2. Mixed monorepo — run the relevant subset per package/area (list areas next if needed)
3. Web frontend + separate API backend (two areas)
4. Mobile/desktop app only (no ZAP unless a web URL appears)
5. Other: _______________

Hints:
- Recommended when `package.json` / `pubspec.yaml` / etc. clearly point to one product root.
- To decide: search for multiple lockfiles, `apps/`, `packages/`, `admin/`, `mobile/`.
- Trade-off: mixed repos need per-area audits; one global command often misses or misreports.
```

### Example — Which web target for ZAP (if any)?

```markdown
### Question
Which web target should OWASP ZAP baseline use (if any)?

1. Localhost / local dev URL only — **Recommended**
2. Staging / non-production URL (user confirms exact URL)
3. Skip ZAP for now (no suitable web target or out of scope)
4. Production URL (only with explicit written confirmation in custom)
5. Other: _______________

Hints:
- Recommended to avoid accidental production load or policy violations.
- To decide: check README start scripts, docker-compose ports, deployed staging docs.
- MUST confirm the exact URL before running. Baseline only — no attack PoCs.
```

### Example — Scope: whole repo vs changed areas only?

```markdown
### Question
What scope should this security tooling run cover?

1. Changed areas / current task paths only — **Recommended** for small scoped work
2. Whole repository (all detected stacks)
3. One package/area only (name it in custom or next question)
4. CI-equivalent full basic set as defined in PROFILE
5. Other: _______________

Hints:
- Recommended during iterative feature work to keep signal high.
- To decide: size of diff, whether this is an existing-project audit (`16`), or first-time baseline.
- Trade-off: full-repo is better for onboarding audits; slower and noisier day-to-day.
```

### Example — Secret scanner preference

```markdown
### Question
Which secret scanner should we prefer?

1. gitleaks — **Recommended**
2. trufflehog (alternate)
3. Skip secrets scan this time
4. Use whatever CI already runs (name it in custom)
5. Other: _______________
```

## New-project workflow

1. Keep `10-security.md` decisions first (auth, secrets storage, roles).
2. Ask whether to enable this tooling module; record status in PROFILE.
3. Detect stacks / monorepo layout; ask to confirm mixed areas if unclear.
4. If web exists, ask ZAP target (prefer localhost/staging).
5. Ask scope (often whole-repo once at bootstrap, then changed-areas later).
6. On approval: run the mapped basic set; send actionable findings into `19-vuln-discovery-and-remediation.md` (then `15-error-handling.md`); wait before fixes.
7. Fill PROJECT-SPECIFIC: enabled tools, targets, excludes.
8. Do not claim “secure” from green scanners alone — still complete `10` review.

## Existing-project workflow

1. Follow `16-existing-projects.md` / `13-ai-review.md` for audit framing.
2. Inventory existing CI scanners; prefer extending them over adding duplicates.
3. Ask enablement + stacks + scope (full-repo baseline often **Recommended** on first AI onboarding audit).
4. Run relevant subset per area; triage findings into `19` remediation plans and the issue/fix plan.
5. Structural secret or authz patterns → root-cause remediation with compatibility notes.
6. Update PROJECT-SPECIFIC with discovered tool commands and exclusions.
7. Quick ignore of a finding only when user chooses that option and residual risk is accepted.

## Post-change checklist hooks

- [ ] Tooling run was approved (or deferred once) before install/execute
- [ ] Stacks detected per area; mixed repo not collapsed to one toolset
- [ ] Dependency audits matched package managers found
- [ ] Secrets + Semgrep applied or explicitly skipped with reason
- [ ] ZAP baseline only, and only with confirmed web target (or skipped)
- [ ] Platform checklists done for mobile/desktop areas in scope
- [ ] Findings entered `19` remediation flow; presented with 4 options + Recommended; user choice before fixes
- [ ] `10-security.md` policy review still completed (tooling did not replace it)
- [ ] PROFILE / PROJECT-SPECIFIC updated when decisions confirmed

## PROJECT-SPECIFIC

- Status: ACTIVE | N/A | PROJECT-SPECIFIC | _______________
- Tooling enabled: yes | no | partial — _______________
- Stacks / areas present: _______________
- Monorepo package paths: _______________
- Dependency auditors in use: _______________
- Secret scanner: gitleaks | trufflehog | other: _______________ | skip
- Semgrep configs / rulesets: _______________
- ZAP baseline target URL(s): _______________ | none
- ZAP allowed environments: localhost | staging | production (explicit): _______________
- Platform checklists required: mobile | desktop | none | _______________
- Optional native tools (if present): _______________
- Default scan scope: changed-areas | whole-repo | per-package: _______________
- Excluded paths: _______________
- CI job names / links: _______________
- N/A rationale: _______________
