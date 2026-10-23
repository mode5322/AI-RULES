# 06 — Database

## Purpose

Keep database decisions explicit. This module is an **always-on reminder/warning layer**: even when marked `N/A`, agents must remain aware that data persistence choices can reappear.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → must be determined; never silently ignored



## When this module applies / when to skip

- Applies whenever data is stored, cached durably, migrated, queried, or modeled.
- If the repo and the current request have no persistence, record `none` and do not ask.
- Keep this file. Re-open the database field only when persistence becomes part of the work.

## Hard rules (MUST / MUST NOT)

- If the repo shows an engine, record it in **System design → Database** in English and do not ask. If there is no database, record `none`. MUST NOT copy connection strings, keys, or passwords.
- A database question uses `templates/question-protocol.md` only when the current task needs a database and the repo does not show the engine.
- MUST use migrations (or the project’s equivalent) for schema changes — no silent production edits by habit.
- MUST NOT store secrets in the database in plaintext.
- MUST consider indexes, constraints, and transactional integrity for multi-step writes.
- MUST keep data-access behind the project’s data layer (see architecture).
- MUST assess DB compatibility after every change that touches models, queries, or migrations.
- MUST NOT use floating-point for money; use integer minor units or a decimal approach the project standardizes.
- Prefer fail-closed permissions on sensitive rows/operations.
- If no database is needed, record `none` and keep this file.

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Ask whether durable storage is needed.
2. If yes: choose engine, hosting, access layer, migrations.
3. Define core entities and constraints before coding features that depend on them.
4. Record the engine in **System design → Database** when this task uses one.
5. If no: set Status `N/A` with reason; continue without inventing a database.

## Existing-project workflow

1. Detect actual DB usage from config, migrations, and data clients. During rules setup, record that engine in **System design → Database** (`00-core.md`).
2. Do not propose a new engine without strong cause.
3. For issues: distinguish data bugs, schema drift, and query bugs.
4. Prefer additive, compatible migrations; avoid destructive changes without backup/confirm.
5. Quick data fix only if isolated; otherwise root-cause with compatibility (see `16-existing-projects.md`).

## Post-change checklist hooks

- [ ] DB module status still correct (ACTIVE vs N/A)
- [ ] Schema/query changes compatible with existing data
- [ ] Migrations included when needed
- [ ] Money/precision rules respected
- [ ] No plaintext secrets persisted

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
