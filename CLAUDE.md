# CLAUDE.md

Instructions for Claude Code / Claude-based agents in a repository that adopted `AI-RULES`.

## Binding rules

Treat everything under `laws/` as mandatory. Start with:

- `laws/00-core.md`
- `templates/question-protocol.md`
- `templates/deferral.md`

Then open the domain files needed for the task (`01`–`19`). For already-built repos, also read `laws/16-existing-projects.md` and `laws/13-ai-review.md`.

## Strict behavior

1. Do not build/start until required clarifying questions and checks are done.
2. Exception: user explicitly defers **for this time only** (`templates/deferral.md`), then restore strict mode.
3. Consuming project: setup and updates use **Install and sync** («ثبّت وزامن», `laws/00-core.md`). Keep configured values and user-added non-pack rules; remove obsolete profile fields; add new pack rules/blanks; sync code-backed System design (`11-change-management.md`). Store an Arabic answer in English. Arabic mixed-script display is a Behavior setting (viewer test on configure).
4. Show the question-protocol option list only when a decision is necessary, it connects to the current project, and the user says «عرض خيارات» or "Show options" (`templates/question-protocol.md`). Otherwise one short line. Do not ask a question the current project does not need. Do not ask deferral or ignore settings. When the user asks to show rule settings and names no category, show the categories only. When the user names **Behavior** or **System design**, list only that category’s settings and values (`laws/00-core.md`, Show settings).
5. Before build/start: state a necessary gap in one short line. Do not open with an option list.
6. A plan that changes pricing or who the product is for gets one short Sales note in `laws/02-discussion.md`. Do not ask for another specialty unless the user asks.
7. Keep database awareness always on (`laws/06-database.md`).
8. After every change: five-point review (modified elements, DB compatibility, logic/math, security, quality/structure).
9. After gates: minimal implementation per `laws/12-code-quality.md` (ladder; intensity lite/full/ultra; never cut validation/security/a11y).
10. On errors: if the user does not know the cause, lead with `problem-brief` (مكان/سبب/حل/حل بديل); then show error + 4 solutions (one Recommended) + custom; wait for choice; prefer root-cause (`laws/15-error-handling.md`).
11. Product UI copy: prefer conversational copy — short, precise, formal (Arabic: فصحى, not dialect); use `.cursor/skills/conversational-copy/` and `laws/04-ux.md`.
12. Branding / app icons: when identity icons or changeable icon packs apply, follow `laws/17-branding-and-icons.md`.
13. Security Laws suite: parent `laws/10-security.md`; tooling + vendored `.cursor/skills/security-audit/` via `laws/18-security-tooling.md`; discovery/remediation `laws/19-vuln-discovery-and-remediation.md` — stack-adaptive; question-gated; plan before fix; wait.
14. Complexity / bloat passes and simplification debt ledger: `laws/13-ai-review.md` and `laws/16-existing-projects.md`.
15. Before mentioning or using a technology, website, reference, feature, algorithm, tool, or library, review its current authoritative source and then work from that (`laws/00-core.md`, Current sources). Do not present an unchecked detail as current.
16. Arabic+Latin chat display follows Behavior → `Arabic mixed-script display`. A stored value is not enough — apply it in every Arabic/RTL reply. On «ضبط قاعدة نص اللغة العربية» (or equivalent), run the viewer test in `laws/00-core.md` (Language) with bare-paragraph samples (never fenced boxes) and store the chosen method in English.
17. Temporary/scratch agent files go under `temp-<operation_name>` (fixed rule in `laws/00-core.md`); do not commit them.
18. When laws conflict, follow Law precedence in `laws/00-core.md`. Resume unfinished setup at the first unconfigured setting. Merge newer pack text without wiping configured values (`laws/11-change-management.md`). Product right-to-left layout is `laws/03-ui.md`.
19. Candor (`laws/00-core.md`, Candor): never open by agreeing; challenge an assumption or expose a gap first. No banned praise phrases. Disagree as "I disagree because … instead … risk …". Uncomfortable truth first; no preamble; change position only on new information.

## Consultant mode

This pack is copied into the user’s project. Record confirmed facts in **Behavior** and **System design** only. Leave the public origin template general/blank.

## Module status

Keep every law file in the tree. Do not ask about a module the current project does not use. Record `none` for a System design part that is absent.

## See also

- `AGENTS.md` — general agent entrypoint
- `README.md` — install and usage
- `USAGE.md` — short playbook
