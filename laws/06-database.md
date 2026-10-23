# 06 — Database

## Purpose

Keep database decisions explicit. This module is an **always-on reminder/warning layer**: even when marked `N/A`, agents must remain aware that data persistence choices can reappear.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → must be determined; never silently ignored

Current: _______________

If `N/A`, reason: _______________

## When this module applies / when to skip

- Applies whenever data is stored, cached durably, migrated, queried, or modeled.
- May be marked `N/A` **only after** questioning confirms the project truly has no DB/persistence need.
- Even when `N/A`, keep this file and re-open questions if persistence appears later.
- ALWAYS determine DB type when status is not firmly `N/A`.

## Hard rules (MUST / MUST NOT)

- MUST determine database type (or confirmed absence) via question protocol before building data features.
- During rules setup on an existing project (`00-core.md`): if the repo already shows the engine, record it in **System design → Database** in English, without asking the user to re-confirm it. MUST NOT copy connection strings, keys, or passwords.
- MUST include a **Recommended** option in every DB question.
- MUST use migrations (or the project’s equivalent) for schema changes — no silent production edits by habit.
- MUST NOT store secrets in the database in plaintext.
- MUST consider indexes, constraints, and transactional integrity for multi-step writes.
- MUST keep data-access behind the project’s data layer (see architecture).
- MUST assess DB compatibility after every change that touches models, queries, or migrations.
- MUST NOT use floating-point for money; use integer minor units or a decimal approach the project standardizes.
- Prefer fail-closed permissions on sensitive rows/operations.
- If no DB is needed: mark `N/A`, document why, keep awareness.

## Question protocol

### Example — Is a database needed?

```markdown
### Question
Does this project need a durable database?

1. Yes — relational SQL database — **Recommended**
2. Yes — document / NoSQL store
3. Yes — local embedded DB only (e.g. SQLite)
4. No durable DB — compute/UI only or external APIs as source of truth
5. Other: _______________

Hints:
- Recommended for business apps with users, records, and reporting.
- If choosing 4, be ready to mark this module N/A and state the source of truth.
```

### Example — Engine choice

```markdown
### Question
Which database engine should we standardize on?

1. PostgreSQL — **Recommended**
2. SQLite
3. MySQL / MariaDB
4. Managed vendor default for our host (specify vendor)
5. Other: _______________

Hints:
- Recommended for multi-user networked apps.
- SQLite is often better for local-first / single-node tools.
```

### Example — Migration discipline

```markdown
### Question
How will schema changes be applied?

1. Versioned migration files in repo — **Recommended**
2. ORM auto-sync in development only (never in production)
3. Manual DBA scripts outside the app repo
4. Serverless/platform schema tool already in use
5. Other: _______________
```

## New-project workflow

1. Ask whether durable storage is needed.
2. If yes: choose engine, hosting, access layer, migrations.
3. Define core entities and constraints before coding features that depend on them.
4. Fill PROJECT-SPECIFIC; set Status `ACTIVE`.
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

- Status: ACTIVE | N/A | _______________
- Engine: _______________
- Hosting: _______________
- ORM / query layer: _______________
- Migration tool: _______________
- Naming conventions (tables/columns): _______________
- Backup / restore notes: _______________
- N/A rationale: _______________
- Sensitive tables / columns: _______________
