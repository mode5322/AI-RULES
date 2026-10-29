# AI-RULES

Public **empty/template origin** of strict AI agent laws. Put this pack into **your** project with one of the two install methods below. The agent then syncs **Behavior** and **System design** for **that project only**. This GitHub origin stays blank/general.

Works for:

1. **Brand-new projects** — gather requirements, discuss, then build under strict gates.
2. **Existing/built projects** — review → rethink → issue/fix plan → fixes (`laws/16-existing-projects.md`).

## What’s inside

| Path | Role |
|---|---|
| `laws/` | Executable protocols `00`–`19` |
| `templates/question-protocol.md` | Canonical clarifying-question format |
| `templates/deferral.md` | One-time deferral wording |
| `templates/project-profile.template.md` | Project truth index (blanks) |
| `AGENTS.md` | General / Codex-oriented entry |
| `CLAUDE.md` | Claude-oriented entry |
| `.cursor/rules/AI-RULES.mdc` | Cursor always-on rule pointing at `laws/` |
| `.cursor/rules/conversational-copy.mdc` | Always-on product UI copy voice |
| `.cursor/skills/conversational-copy/` | Skill: short precise formal UI copy (Arabic: فصحى) |
| `.cursor/skills/problem-brief/` | Skill: short diagnosis brief when the user does not know the cause |
| `.cursor/skills/security-audit/` | Vendored multi-phase security audit skill (Cloudflare MIT upstream) |
| `.cursor/rules/problem-brief.mdc` | Always-on problem-brief format (bare paragraphs; no code box) |
| `.cursor/rules/arabic-mixed-script.mdc` | Always-on fixed marks: U+200F + LRI/PDI; pre-reply review |
| `.cursor/rules/candor.mdc` | Always-on candor: no opening agreement, structured disagreement |

## How to use

Setup is one of two methods. Both finish with the same agent command: install and sync (`laws/00-core.md`, Install and sync).

### Method 1 — copy the rules folder

1. Copy the rules pack folder (the folder that contains `laws/`) into the root of the consuming project.
2. In a chat inside that project, tell the agent: «ثبّت وزامن القواعد من مجلد القواعد على المشروع الحالي».

### Method 2 — send the repository link

Send the agent the repository URL and the install command in one message:

> ثبّت وزامن قواعد هذا المستودع مع المشروع الحالي
> https://github.com/mode5322/AI-RULES

The agent fetches the pack, places `laws/` and `templates/` at the project root, and syncs **Behavior** and **System design** from the current project. It writes values the code already shows, in English. It records `none` for a part the project does not use, and it does not ask about that part. It does not push the filled project back to the rules repository.

### After sync

- **Existing project:** follow `laws/16-existing-projects.md` (review, then a fix plan). Do not patch first.
- **New project:** implement only after the one question this request still needs, if any.
- A later chat must continue at the first relevant unset field. It must not restart finished sections, re-ask values that are already set, or open a field the project does not use. It must also confirm `arabic-mixed-script.mdc` and run the pre-reply mark review on the first Arabic reply (`laws/00-core.md`, Resume).
- Arabic+Latin chat marks are **fixed** (U+200F every Arabic line; U+2066…U+2069 every Latin term) — not a Behavior setting. Product right-to-left layout is a separate rule (`laws/03-ui.md`).
- Agent temporary files use `temp-<operation_name>` folders (fixed rule in `laws/00-core.md`); ignored via `temp-*/` in `.gitignore`.
- Domain laws `01`–`19` open when the task needs that file. They are not a second setup walk.

### Bring a newer pack into a project that is already synced

Run method 1 or method 2 again with the same «ثبّت وزامن» / "Install and sync" phrases. That command already includes the merge contract (`laws/00-core.md`, Install and sync; `laws/11-change-management.md`):

1. Keep every configured **Behavior** / **System design** value.
2. Keep rules/skills the user added that are not part of this pack.
3. Delete obsolete profile fields that no longer exist in the newer `templates/project-profile.template.md`.
4. Add new laws, hard rules, and new profile blanks — including always-on `arabic-mixed-script.mdc` (sync incomplete if missing). Remove retired field `Arabic mixed-script display`.
5. Ask only about a new relevant blank the project uses.
6. State the source revision in the reply. Do not push the filled copy back to this public origin.

### One-time skip

To skip setup for the current task only, say that you defer **for this time only**. The gate returns on the next task. That sentence is not the same as the agent holding work until setup is done.

Shorter install notes are also in `USAGE.md`.

## Core behaviors (encoded in laws)

- **English only** for law file content. Arabic mixed-script chat marks are fixed in `laws/00-core.md` (U+200F / U+2066…U+2069; pre-reply review).
- **Four operating additions** — law precedence and setup resume (`laws/00-core.md`); upstream merge that keeps filled settings (`laws/11-change-management.md`); product right-to-left layout separate from chat lines (`laws/03-ui.md`).
- **Current sources** — before a technology, website, reference, feature, algorithm, tool, or library is mentioned or used, its authoritative source is reviewed and the work follows what that source says now (`laws/00-core.md`).
- **Very strict** — no execution until required questions/checks complete, except explicit **for this time only** deferral.
- **Install and sync** («ثبّت وزامن») — the only setup entry and the update path. Keeps configured values and user-added non-pack rules; removes obsolete profile fields; adds new pack rules/blanks; syncs code-backed System design. See `laws/00-core.md` and `laws/11-change-management.md`.
- **Question protocol** — the option list appears only when a decision is necessary and the user says «عرض خيارات» or "Show options". Otherwise one short line. Deferral and ignore settings are not asked (`templates/question-protocol.md`, `templates/deferral.md`).
- **Show settings** — «عرض الإعدادات» shows the categories only, plus a completed/remaining table. Naming a category, such as «عرض إعدادات قواعد السلوك» or «عرض إعدادات قواعد تصميم النظام», lists only that category’s settings and values (`laws/00-core.md`).
- **Rules-setup modes** — `strict-hold` (default: hold work until configured) or `configure-on-request` (configure only when asked; no hold for blanks). Fixed phrase for the latter: "Stop the question protocol until I ask to configure the rules" (see `templates/deferral.md`).
- **When to ask** — one short line only when a decision is necessary. The option list waits for «عرض خيارات» or "Show options".
- **UI** — match the existing interface. Do not open a questionnaire for buttons, icons, menus, or colors (`laws/03-ui.md`).
- **Discussion** — one Sales note only when the plan changes pricing or who the product is for (`laws/02-discussion.md`).
- **Database** — awareness stays on. Record the engine the repo shows, or `none` when there is no database, without a question (`laws/06-database.md`).
- **Branding / icons** — desktop, mobile, and web identity assets; static vs user-changeable (`laws/17-branding-and-icons.md`).
- **Security Laws suite** — parent policy (`laws/10-security.md`) + tooling (`laws/18-security-tooling.md`, including `.cursor/skills/security-audit/`) + discovery/remediation (`laws/19-vuln-discovery-and-remediation.md`); plan before fix; wait.
- **After every change** — review modified elements, DB compatibility, logic/math, security, quality/structure.
- **Minimal implementation** — after gates, follow the ladder in `laws/12-code-quality.md` (YAGNI → stdlib → native → installed deps → fewest lines); intensity lite/full/ultra; never cut validation/security/accessibility/data-loss handling. Merged into laws — not a separate pack.
- **Complexity / debt passes** — optional over-engineering tags + simplification markers ledger (`laws/13-ai-review.md`, `laws/16-existing-projects.md`).
- **Errors** — show immediately + 4 solutions (one Recommended) + custom; wait before fixing; prefer root-cause.

## Marking modules N/A

If a module does not connect to the current project, leave its file in the tree and do not ask about it. Record `none` for a System design part the project does not use. Do not add a reason blank in the law file.

## License

MIT — see `LICENSE`.
