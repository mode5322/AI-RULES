# strict-ai-rules

Public **empty/template origin** of strict AI agent laws. Copy this pack into **your** project. Inside your project, the AI acts as a consultant: it fills and customizes the law files for **that project only**. This GitHub origin stays blank/general.

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
| `.cursor/rules/strict-ai-rules.mdc` | Cursor always-on rule pointing at `laws/` |
| `.cursor/rules/conversational-copy.mdc` | Always-on product UI copy voice |
| `.cursor/skills/conversational-copy/` | Skill: short precise formal UI copy (Arabic: فصحى) |
| `.cursor/skills/problem-brief/` | Skill: short diagnosis brief when the user does not know the cause |
| `.cursor/rules/problem-brief.mdc` | Always-on problem-brief format |
| `.cursor/rules/candor.mdc` | Always-on candor: no opening agreement, confidence tags, structured disagreement |

## How to use

### 1. Install into the project root

Copy these into the **root** of the consuming project (a new app or an existing one):

- `laws/`
- `templates/`
- `AGENTS.md`
- `CLAUDE.md`
- `.cursor/rules/strict-ai-rules.mdc`

The Cursor rule file is what makes that editor load the laws on every task. Do not leave the pack in a subfolder the agent will not read.

Fill settings only in that project copy. This public origin stays blank.

### 2. Configure the rules before any other work

Open a **new chat inside that project** and ask the agent to configure the rules. Say whether the project is new or already built.

The agent holds every other request until the **relevant** **Behavior** and **System design** fields are filled (`templates/project-profile.template.md`). A field the project does not use is recorded as `none` and is not asked, unless the user asks to see it. Questions are in the user’s language. An Arabic answer is stored in English. The Arabic line-split is fixed and is not a setting. One relevant field per turn.

- **Existing project:** database, framework, external connection, and libraries that the code already shows are written in English without asking again. A part the project does not use is recorded as `none` and is not asked.
- **New project:** the agent asks only for the fields the current request needs. It records `none` for unused parts and does not invent facts.

A relevant blank, `not set`, `undecided`, or `TBD` is not configured. A field the project does not use is `none` and is not a question.

### 3. After setup is complete

- **Existing project:** follow `laws/16-existing-projects.md` (review, then a fix plan). Do not patch first.
- **New project:** implement only after the blocking questions for that work are answered.
- A later chat must continue at the first relevant unset field. It must not restart finished sections, re-ask values that are already set, or open a field the project does not use (`laws/00-core.md`, Resume).
- Arabic chat replies keep each Arabic sentence on its own line and each English term on its own line. Product right-to-left layout is a separate rule (`laws/03-ui.md`).

### 4. Bring newer laws into a project that is already configured

`git pull` updates files. It does not run the agent, and it does not know that filled settings must be kept.

- If this pack was **copied** into the larger project, `git pull` on the larger project does not fetch this repository. Copy the newer pack in, then tell the agent to sync.
- If `strict-ai-rules` is its **own clone or submodule** inside the larger project, `git pull` inside that folder updates the law text only. It can overwrite filled lines with blanks, or stop on a conflict. After the pull, tell the agent to sync.

Say this:

> Sync the new upstream rules with the rules already configured in this project. Do not erase a configured value. Add the new settings only, and ask about those.

The agent must then (`laws/11-change-management.md`, Upstream law merge):

1. Keep every configured value.
2. Add new laws and new blank settings from the newer pack.
3. Ask only about the new blanks.
4. Record the upstream revision in the project profile.
5. Leave the filled copy in the consuming project. Do not push it back to this public origin.

### 5. One-time skip

To skip setup for the current task only, say that you defer **for this time only**. The gate returns on the next task. That sentence is not the same as the agent holding work until setup is done.

Shorter install notes are also in `USAGE.md`.

## Core behaviors (encoded in laws)

- **English only** for law file content. In an Arabic conversation, each Arabic sentence is its own line and each English word or term is its own line, so the Arabic line does not reverse (`laws/00-core.md`).
- **Four operating additions** — law precedence and setup resume (`laws/00-core.md`); upstream merge that keeps filled settings (`laws/11-change-management.md`); product right-to-left layout separate from chat lines (`laws/03-ui.md`).
- **Current sources** — before a technology, website, reference, feature, algorithm, tool, or library is mentioned or used, its authoritative source is reviewed and the work follows what that source says now (`laws/00-core.md`).
- **Very strict** — no execution until required questions/checks complete, except explicit **for this time only** deferral.
- **Rules-setup gate** — work is held until the **relevant** **Behavior** and **System design** fields are configured. A field the project does not use is not asked unless the user asks to see it. Questions use the user’s language. Arabic answers are stored in English. Code-backed database, framework, connection, and libraries are recorded automatically. A new library is added only when the user asks for something the installed libraries do not provide. See `laws/00-core.md`.
- **Question protocol** — the option list appears only when a decision is necessary and the user says «عرض خيارات» or "Show options". Otherwise one short line. Deferral and ignore settings are not asked (`templates/question-protocol.md`, `templates/deferral.md`).
- **Incomplete settings** — when asked, every **relevant** remaining setting is numbered from 1 through the full count, then a category table shows completed and remaining. Unrelated blanks stay hidden unless the user asks to see them (`laws/00-core.md`).
- **Rules-setup modes** — `strict-hold` (default: hold work until configured) or `configure-on-request` (configure only when asked; no hold for blanks). Fixed phrase for the latter: "Stop the question protocol until I ask to configure the rules" (see `templates/deferral.md`).
- **When to ask** — one short line only when a decision is necessary. The option list waits for «عرض خيارات» or "Show options".
- **UI** — not a fixed visual identity; question protocol for buttons, icons, menus, containers, aesthetics when unclear.
- **Discussion** — new plans get brief CEO + HR + Sales angles; ask if another specialty is needed.
- **Database** — always-on awareness; determine DB type; `N/A` only after questioning.
- **Branding / icons** — desktop, mobile, and web identity assets; static vs user-changeable (`laws/17-branding-and-icons.md`).
- **Security Laws suite** — parent policy (`laws/10-security.md`) + optional defensive tooling (`laws/18-security-tooling.md`) + authorized discovery/remediation (`laws/19-vuln-discovery-and-remediation.md`); no exploits.
- **After every change** — review modified elements, DB compatibility, logic/math, security, quality/structure.
- **Minimal implementation** — after gates, follow the ladder in `laws/12-code-quality.md` (YAGNI → stdlib → native → installed deps → fewest lines); intensity lite/full/ultra; never cut validation/security/accessibility/data-loss handling. Merged into laws — not a separate pack.
- **Complexity / debt passes** — optional over-engineering tags + simplification markers ledger (`laws/13-ai-review.md`, `laws/16-existing-projects.md`).
- **Errors** — show immediately + 4 solutions (one Recommended) + custom; wait before fixing; prefer root-cause.

## Marking modules N/A

If a module truly does not apply (e.g. no database after questioning):

1. Set Status to `N/A`.
2. Write the reason in the module’s PROJECT-SPECIFIC / status fields.
3. Keep the file — it remains a reminder/warning layer (especially `06-database.md`).

## License

MIT — see `LICENSE`.
