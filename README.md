# strict-ai-rules

Public **empty/template origin** of strict AI agent laws. Copy this pack into **your** project. Inside your project, the AI acts as a consultant: it fills and customizes the law files for **that project only**. This GitHub origin stays blank/general.

Works for:

1. **Brand-new projects** — gather requirements, discuss, then build under strict gates.
2. **Existing/built projects** — review → rethink → issue/fix plan → fixes (`laws/16-existing-projects.md`).

## What’s inside

| Path | Role |
|---|---|
| `laws/` | Executable protocols `00`–`16` |
| `templates/question-protocol.md` | Canonical clarifying-question format |
| `templates/deferral.md` | One-time deferral wording |
| `templates/project-profile.template.md` | Project truth index (blanks) |
| `AGENTS.md` | General / Codex-oriented entry |
| `CLAUDE.md` | Claude-oriented entry |
| `.cursor/rules/strict-ai-rules.mdc` | Cursor always-on rule pointing at `laws/` |

## Quick start

1. Copy this repository into your project root (clone, subtree, or copy folders).
2. Keep `laws/`, `templates/`, and the IDE entry files you need.
3. Ask your agent to read `AGENTS.md` / `laws/00-core.md` and fill `PROJECT-SPECIFIC` sections for your app.
4. Mark modules `ACTIVE`, `N/A`, or leave `PROJECT-SPECIFIC` with notes.
5. For existing apps, start with `laws/16-existing-projects.md` — do not patch first.

See `USAGE.md` for a short install playbook.

## Core behaviors (encoded in laws)

- **English only** for law file content.
- **Very strict** — no execution until required questions/checks complete, except explicit **for this time only** deferral.
- **Question protocol** — 1 question, 4 options, option 5 custom blank, one **Recommended**, optional research hints.
- **When to ask** — always before build/start; during/after only if ambiguous (unless deferred).
- **UI** — not a fixed visual identity; question protocol for buttons, icons, menus, containers, aesthetics when unclear.
- **Discussion** — new plans get brief CEO + HR + Sales angles; ask if another specialty is needed.
- **Database** — always-on awareness; determine DB type; `N/A` only after questioning.
- **After every change** — review modified elements, DB compatibility, logic/math, security, quality/structure.
- **Errors** — show immediately + 4 solutions (one Recommended) + custom; wait before fixing; prefer root-cause.

## Marking modules N/A

If a module truly does not apply (e.g. no database after questioning):

1. Set Status to `N/A`.
2. Write the reason in the module’s PROJECT-SPECIFIC / status fields.
3. Keep the file — it remains a reminder/warning layer (especially `06-database.md`).

## License

MIT — see `LICENSE`.
