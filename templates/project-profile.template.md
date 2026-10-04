# Project Profile Template

Copy this into the consuming project (or fill the PROJECT-SPECIFIC sections inside `laws/`). Leave blanks empty until customized for **this** project. Do not fill blanks in the public origin template beyond placeholders.

## Rules setup

Filled only in a consuming project (`laws/00-core.md`). Setup is `complete` only when every field in this profile and every `PROJECT-SPECIFIC` setting in the laws and templates is configured. Leave these blank on the public origin. A blank or `not set` is not configured.

- Status: not-started | in-progress | complete | _______________
- Held first request (unexecuted): _______________
- Last finished section: _______________
- Next section: _______________
- Upstream revision merged: _______________
- Upstream merge notes: _______________

## Identity

- Project name: _______________
- Primary language(s): _______________
- Stack / framework: _______________
- Platform(s): web | mobile | desktop | API | CLI | other: _______________
- Locale / UI language: _______________
- Repo status: brand-new | existing / introduced-AI-later

## Product

- Problem solved: _______________
- Primary users: _______________
- Non-goals: _______________
- Compliance constraints: _______________

## Architecture

- Architecture style: _______________
- Monorepo / multi-package: yes | no | _______________
- Key folders (screens, services, database, etc.): _______________
- Shared libraries / design system: _______________
- Minimal-implementation intensity (lite | full | ultra): _______________
- Simplification marker prefix (`simplify:` / `ponytail:` / other): _______________

## Branding and icons

- Module status: ACTIVE | N/A | PROJECT-SPECIFIC | undecided
- Platform type(s): desktop | mobile | web | multi: _______________
- Icon strategy: static | changeable-pack | changeable-pack+upload | build-time flavors | _______________
- Icon set location (source of truth): _______________
- Default icon (filename or id): _______________
- Generated / platform export paths: _______________
- Why N/A (if marked): _______________

## Database

- Module status: ACTIVE | N/A | undecided
- Database type: _______________
- ORM / query layer: _______________
- Migration tool: _______________
- Hosting: _______________
- Why N/A (if marked): _______________

## Security Laws suite (see `laws/10-security.md` — parent)

Parent policy / access (`10`):

- Auth method: _______________
- Roles / RBAC model: _______________
- Secrets storage: _______________
- Threat notes: _______________

### Defensive tooling (`18` — see `laws/18-security-tooling.md`)

- Module status: ACTIVE | N/A | PROJECT-SPECIFIC | undecided
- Tooling enabled: yes | no | partial | _______________
- Stacks / areas present: _______________
- Monorepo package paths: _______________
- Web target URL(s) for ZAP baseline: _______________ | none
- Tools enabled: deps-audit | gitleaks | trufflehog | semgrep | zap-baseline | platform-checklists | _______________
- Default scan scope: changed-areas | whole-repo | per-package: _______________
- Excluded paths: _______________
- Why N/A (if marked): _______________

### Vuln discovery & remediation (`19` — see `laws/19-vuln-discovery-and-remediation.md`)

- Module status: ACTIVE | N/A | PROJECT-SPECIFIC | undecided
- Suite enablement noted under `10`: yes | no | _______________
- Authorized discovery targets: this-repo | localhost | staging URLs: _______________ | none
- Production scan allowed: no | yes (explicit only): _______________
- Discovery cadence: on-audit | per-PR / changed-areas | scheduled: _______________ | ad-hoc
- Default discovery inputs: `18` tooling | AI review (`10`/`13`) | both | _______________
- Extra scanners beyond `18` (e.g. Nuclei opt-in): _______________ | none (default)
- Finding log / issue tracker path: _______________
- Why N/A (if marked): _______________

## Quality gates

- Required tests before merge: _______________
- Linters / formatters: _______________
- Review checklist owners: _______________

## Existing-project notes (if applicable)

- Audit date: _______________
- Known issue themes: _______________
- Remediation plan link / path: _______________
- Compatibility constraints: _______________

## Module status map

| Law module | Status (ACTIVE / N/A / PROJECT-SPECIFIC) | Notes |
|---|---|---|
| 00-core | ACTIVE | |
| 01-requirements | | |
| 02-discussion | | |
| 03-ui | | |
| 04-ux | | |
| 05-architecture | | |
| 06-database | | |
| 07-logic-and-math | | |
| 08-validation | | |
| 09-testing | | |
| 10-security | | Security Laws suite parent |
| 11-change-management | | |
| 12-code-quality | | |
| 13-ai-review | | |
| 14-final-verification | | |
| 15-error-handling | | |
| 16-existing-projects | | |
| 17-branding-and-icons | | |
| 18-security-tooling | | Security Laws companion (tools) |
| 19-vuln-discovery-and-remediation | | Security Laws companion (discover→remediate) |

## Custom laws

- Extra project laws path(s): _______________
- Overrides (document carefully): _______________
