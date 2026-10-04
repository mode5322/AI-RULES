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
3. Consuming project with incomplete rules setup: hold the first request, propose configuring the agent rules, then walk one section per turn (`00`–`19`) until all are finished (`laws/00-core.md`). Existing repo: record general facts the code already shows (database such as Firebase, Supabase, or SQL). New repo: ask; do not invent facts.
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

## Consultant mode

This pack is copied into the user’s project. Customize PROJECT-SPECIFIC sections for **this** project. Leave the public origin template general/blank.

## Module status

Modules may be `ACTIVE`, `N/A`, or `PROJECT-SPECIFIC`. Mark `N/A` only when questioning shows the module truly does not apply (especially database). Keep N/A modules in tree as reminders.

## See also

- `AGENTS.md` — general agent entrypoint
- `README.md` — install and usage
- `USAGE.md` — short playbook
