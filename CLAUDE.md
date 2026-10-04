# CLAUDE.md

Instructions for Claude Code / Claude-based agents in a repository that adopted `strict-ai-rules`.

## Binding rules

Treat everything under `laws/` as mandatory. Start with:

- `laws/00-core.md`
- `templates/question-protocol.md`
- `templates/deferral.md`

Then open the domain files needed for the task (`01`–`19`). For already-built repos, also read `laws/16-existing-projects.md` and `laws/13-ai-review.md`.

## Strict behavior

1. Do not build/start until required clarifying questions and checks are done.
2. Exception: user explicitly defers **for this time only** (`templates/deferral.md`), then restore strict mode.
3. Consuming project: configure every setting in laws `00`–`19`, template `PROJECT-SPECIFIC` bullets, and the project profile before product or code work (`laws/00-core.md`). Hold the request while any setting is blank. One section at a time, one unconfigured setting per turn. Existing repo: record values the code already shows (database such as Firebase, Supabase, or SQL, and any other plain fact), then ask for the rest. New repo: ask; do not invent facts. Do not skip a setting with `not set`.
4. Clarifying questions always use: 1 question, 4 options, option 5 custom blank, one **Recommended**, optional research hints.
5. Before build/start: always ask what is required. During/after: only if ambiguous.
6. Any new plan: short CEO + HR + Sales angles, then ask if another specialty is needed (`laws/02-discussion.md`).
7. Keep database awareness always on (`laws/06-database.md`).
8. After every change: five-point review (modified elements, DB compatibility, logic/math, security, quality/structure).
9. After gates: minimal implementation per `laws/12-code-quality.md` (ladder; intensity lite/full/ultra; never cut validation/security/a11y).
10. On errors: show error + 4 solutions (one Recommended) + custom; wait for choice; prefer root-cause (`laws/15-error-handling.md`).
11. Branding / app icons: when identity icons or changeable icon packs apply, follow `laws/17-branding-and-icons.md`.
12. Security Laws suite: parent `laws/10-security.md`; optional defensive tooling `laws/18-security-tooling.md`; authorized discovery/remediation `laws/19-vuln-discovery-and-remediation.md` — stack-adaptive; question-gated; plan before fix; wait; no exploits.
13. Complexity / bloat passes and simplification debt ledger: `laws/13-ai-review.md` and `laws/16-existing-projects.md`.
14. Before mentioning or using a technology, website, reference, feature, algorithm, tool, or library, review its current authoritative source and then work from that (`laws/00-core.md`, Current sources). Do not present an unchecked detail as current.
15. In an Arabic conversation, put each Arabic sentence on its own line and each English word or term on its own line (`laws/00-core.md`, Language). Do not embed an English term inside an Arabic line.
16. When laws conflict, follow Law precedence in `laws/00-core.md`. Resume unfinished setup at the first unconfigured setting. Merge newer pack text without wiping configured values (`laws/11-change-management.md`). Product right-to-left layout is `laws/03-ui.md`.

## Consultant mode

This pack is copied into the user’s project. Customize PROJECT-SPECIFIC sections for **this** project. Leave the public origin template general/blank.

## Module status

Modules may be `ACTIVE`, `N/A`, or `PROJECT-SPECIFIC`. Mark `N/A` only when questioning shows the module truly does not apply (especially database). Keep N/A modules in tree as reminders.

## See also

- `AGENTS.md` — general agent entrypoint
- `README.md` — install and usage
- `USAGE.md` — short playbook
