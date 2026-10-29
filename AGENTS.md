# AGENTS.md

Instructions for coding agents (Codex, Cursor Agent, and general LLM agents) working in a repository that includes this template.

## What this is

`AI-RULES` is a **strict law pack** for AI agents. After this folder is copied into a **user project**, agents must treat `laws/` as binding operating rules and record confirmed facts in **Behavior** and **System design** only.

The public GitHub origin stays a blank/general template.

## Mandatory read order

Before non-trivial work, read:

1. `laws/00-core.md`
2. `templates/question-protocol.md`
3. `templates/deferral.md`
4. Then domain laws as relevant (`01`–`19`)
5. For existing codebases: `laws/16-existing-projects.md` and `laws/13-ai-review.md`

## Operating summary

- English-only law content. Arabic+Latin chat marks are **fixed** (U+200F every Arabic line; U+2066…U+2069 every Latin term) via `.cursor/rules/arabic-mixed-script.mdc` — pre-reply review before every Arabic/RTL send; never fence `problem-brief`.
- Temporary/scratch agent files go under `temp-<operation_name>` (fixed rule in `laws/00-core.md`); do not commit them.
- Candor (`laws/00-core.md`, Candor): never open by agreeing; the first sentence challenges an assumption, exposes a gap, or asks a revealing question. No "Great question" / "You're absolutely right" / "Certainly" / "Absolutely". Disagree as "I disagree because … instead … risk …". Uncomfortable truth first; no preamble; change position only on new information.
- When laws conflict, follow Law precedence in `laws/00-core.md`. A new chat resumes at the first unconfigured setting and does not re-ask configured ones. Merging a newer pack keeps configured values (`laws/11-change-management.md`). Product right-to-left layout is `laws/03-ui.md`, not conversation bidi isolation.
- Before mentioning or using any technology, website, reference, feature, algorithm, tool, or library, review its current authoritative source, then work from that (`laws/00-core.md`, Current sources). If the source cannot be reviewed, do not present the detail as current.
- Very strict: do not execute until required questions/checks complete, unless the user defers **for this time only**.
- Consuming project: setup and later updates use **Install and sync** only («ثبّت وزامن», `laws/00-core.md`). Keeps configured values and user-added non-pack rules; removes obsolete profile fields (including retired `Arabic mixed-script display`); adds pack rules including `arabic-mixed-script.mdc`; syncs code-backed System design (`11-change-management.md`). Do not push the filled project to the rules repository.
- Question protocol option lists appear only when a decision is necessary and the user says «عرض خيارات» or "Show options" (`templates/question-protocol.md`). Otherwise one short line. Do not ask deferral or ignore settings.
- When the user asks to show rule settings and names no category, show the categories only, then the completed/remaining table. When the user names **Behavior** or **System design**, including «عرض إعدادات قواعد السلوك» and «عرض إعدادات قواعد تصميم النظام», list only that category’s settings and their current values (`laws/00-core.md`, Show settings).
- Rules-setup mode: `strict-hold` (default) or `configure-on-request` (configure only when asked; do not hold product work for blanks). Fixed phrase for the latter: "Stop the question protocol until I ask to configure the rules" / «إيقاف بروتوكول الأسئلة إلى أن أطلب ضبط إعدادات القواعد» (`templates/deferral.md`).
- A plan that changes pricing or who the product is for: one short Sales note in `laws/02-discussion.md`. Do not ask for another specialty unless the user asks.
- Database type is asked only when the project has a database or the current request needs one. Otherwise record `none` and do not ask (`laws/06-database.md`).
- After every change: review modified elements, DB compatibility, logic/math, security, quality/structure.
- Minimal implementation (merged into laws, not a separate pack): after gates, use the `12` ladder (YAGNI → stdlib → native → installed dep → fewest lines); never cut validation/security/a11y/data-loss handling; intensity lite/full/ultra (default full).
- Complexity review tags + simplification debt ledger live in `13` / `16` (optional passes).
- Errors: if the user does not know the cause, lead with skill `problem-brief` (مكان/سبب/حل/حل بديل); then show 4 solutions (one Recommended) + custom; **wait** before fixing; prefer root-cause.
- Existing projects: review → rethink → issue/fix plan → fixes (`16-existing-projects.md`).
- Product UI copy: prefer **conversational copy** — short, precise, formal (Arabic: فصحى, not dialect); use skill `.cursor/skills/conversational-copy/` and `laws/04-ux.md` voice rules.
- Branding / app icons: follow `17-branding-and-icons.md` when identity icons, favicons, launcher/PWA/store assets, or user-changeable icon packs are in scope.
- Security Laws suite (`10` + `18` + `19`): parent policy `10-security.md`; optional scanners + vendored `.cursor/skills/security-audit/` via `18-security-tooling.md`; authorized discovery → remediation `19-vuln-discovery-and-remediation.md` (plan before fix; wait).

## Do / Don’t

- DO record a confirmed Behavior or System design fact in the project profile.
- DO leave a law file in the tree when the project does not use that module.
- DON’T invent project facts in the public origin template.
- DON’T add a fill-in setting outside the profile.
- DON’T commit unless the user explicitly asks.

## Profile

Prefer filling `templates/project-profile.template.md` (or equivalent project copy) as the index of project truths.
