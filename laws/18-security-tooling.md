# 18 — Security Tooling

## Purpose

Add an **optional tooling layer** that supplements — never replaces — the policy and AI security review in `10-security.md`. This module is a **Security Laws** companion under parent `10` (suite: `10` policy → `18` tools → `19` discovery/remediation). Tools adapt to detected project type / stack, including **mixed monorepos** (e.g. Flutter app + React admin + static web). Agents run scanners and deep audits only after the user asks for that work (or one-time deferral per `templates/deferral.md`).

Actionable findings from this module **MUST feed into** `19-vuln-discovery-and-remediation.md` (triage → Remediation Closure Plan → wait → fix) — not silent auto-fix.

This module has two discovery tracks:

**A — Basic scanners**

1. Dependency auditors (package-manager native where available)
2. Secret scanners (`gitleaks` preferred; `trufflehog` alternate)
3. Light SAST (`semgrep` with community / OWASP-oriented configs)
4. OWASP ZAP **Baseline only** — web targets only, after scope confirmation
5. Platform rule-based checks for mobile/desktop (checklist-driven; optional native tools if already present)

**B — Multi-phase security-audit skill (vendored)**

6. Cursor skill at `.cursor/skills/security-audit/` (from Cloudflare `security-audit-skill`, MIT). Use for explicit codebase security audits / pen-test-style reviews. Follow that skill’s phases, sandbox rules, validators, and `findings.json` schema. See `ORIGIN.md` in the skill folder.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`



## When this module applies / when to skip

- Applies when the user opts into defensive scans, when PROFILE enables tooling, or when a security review (`10`, `13`, `16`) recommends automated checks.
- Applies on new-project security setup and on existing-project audits — depth scales with risk and user choice.
- Skip running tools unless the user asked for that scan. Also skip when the user declined tooling for this session, there is no runnable target, or the scope is docs only.
- MUST NOT treat tooling as a substitute for `10-security.md` review (secrets, authz, validation, least privilege).
- Cross-links: policy/review → `10-security.md`; findings presentation → `15-error-handling.md`; discovery findings MUST enter remediation → `19-vuln-discovery-and-remediation.md`; existing audits → `16-existing-projects.md` / `13-ai-review.md`; functional tests ≠ security scans → `09-testing.md`.

## Hard rules (MUST / MUST NOT)

### Tooling classes

- MUST use track **A** (basic scanners) and/or track **B** (`.cursor/skills/security-audit/`) when the user asks for security scanning or a full audit.
- For track **B**, MUST follow `.cursor/skills/security-audit/SKILL.md` (modes, sandbox, write isolation, validators). That skill is an approved discovery path in this pack — not a forbidden parallel stack.
- MUST NOT expand ZAP beyond **baseline** mode in track **A** unless the user explicitly asks for a deeper ZAP mode.
- Nuclei or similar template-driven scanners: enable only when the user explicitly asks, limited to confirmed localhost or staging.

### Gate before running

- MUST ask via `templates/question-protocol.md` before installing or running security tools, unless the user deferred **for this time only** or already asked for a security audit / pen-test in clear terms (that request authorizes track **B**).
- MUST confirm stacks present, scan scope (whole repo vs changed areas), and any web target URL before ZAP baseline.
- MUST prefer localhost / staging targets over production; MUST get explicit confirmation before scanning any non-local URL.
- MUST wait for user choice before acting on finding remediations (discovery may proceed once authorized).

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

- Run a scanner only when the user asks for that scan. Do not add a settings blank for the tool list.
- MUST NOT commit scanner credentials, API tokens for commercial scanners, or raw reports that embed secrets.
- Prefer read-only / non-destructive scan modes; do not mutate production data as part of a scan.

## Stack detection / mapping matrix

Detect by lockfiles, manifests, and folder layout. Apply the union of rows that match. Commands are **high-level names** (install/run); adapt to OS and local PATH. Track **B** (security-audit skill) is stack-agnostic and may run alongside this matrix.

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

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Keep `10-security.md` decisions first (auth, secrets storage, roles).
2. Ask whether to enable this tooling module; record status in PROFILE.
3. Detect stacks / monorepo layout; ask to confirm mixed areas if unclear.
4. If web exists, ask ZAP target (prefer localhost/staging).
5. Ask scope (often whole-repo once at bootstrap, then changed-areas later).
6. On approval: run track **A** and/or track **B** as requested; send actionable findings into `19-vuln-discovery-and-remediation.md` (then `15-error-handling.md`); wait before fixes.
7. Do not add a settings blank for tools or targets.
8. Do not claim “secure” from green scanners alone — still complete `10` review.

## Existing-project workflow

1. Follow `16-existing-projects.md` / `13-ai-review.md` for audit framing.
2. Inventory existing CI scanners; prefer extending them over adding duplicates.
3. Ask enablement + stacks + scope (full-repo baseline often **Recommended** on first AI onboarding audit).
4. Run relevant subset per area; triage findings into `19` remediation plans and the issue/fix plan.
5. Structural secret or authz patterns → root-cause remediation with compatibility notes.
6. Use the scanner command the repo already has. Do not add a settings blank.
7. Quick ignore of a finding only when user chooses that option and residual risk is accepted.

## Post-change checklist hooks

- [ ] Tooling run was approved (or deferred once) before install/execute
- [ ] Stacks detected per area; mixed repo not collapsed to one toolset
- [ ] Dependency audits matched package managers found
- [ ] Secrets + Semgrep applied or explicitly skipped with reason (when track A is in scope)
- [ ] ZAP baseline only (unless user asked for more), and only with confirmed web target (or skipped)
- [ ] Platform checklists done for mobile/desktop areas in scope (when relevant)
- [ ] Track B (`security-audit` skill) used when the user asked for a full audit / pen-test-style review
- [ ] Findings entered `19` remediation flow; presented with 4 options + Recommended; user choice before fixes
- [ ] `10-security.md` policy review still completed (tooling did not replace it)
- [ ] No scanner/audit ran unless the user asked for that work

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
