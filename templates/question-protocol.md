# Question Protocol (Canonical)

Use this format for **every** clarifying question before work proceeds.

## Rules

1. Ask **exactly one** question at a time.
2. Offer **exactly four** concrete answer options.
3. Offer **option 5** as a custom blank the user can fill.
4. Mark **exactly one** of options 1–4 as **Recommended**.
5. When helpful, add short **research-friendly suggestion hints** under options (search terms, docs to check, or trade-offs). If a hint states how a technology, website, reference, feature, algorithm, tool, or library works, review its current authoritative source first (`laws/00-core.md`, Current sources).
6. Wait for the user's choice (or custom answer) before continuing. If the question is asked in Arabic, follow the line split in `laws/00-core.md` (Language): Arabic on its own line, each English term on its own line.
7. Do not batch multiple independent questions into one message unless the user explicitly deferred clarification for this time only (see `templates/deferral.md`).

## Template

```markdown
### Question
<one clear question>

1. <option A>
2. <option B> — **Recommended**
3. <option C>
4. <option D>
5. Other: _______________

Hints (optional):
- Recommended because: <one short reason>
- To decide: search `<term>` / check `<doc or file>`
- Trade-off: <A vs B in one line>
```

## Example

```markdown
### Question
Which primary database should this project use?

1. PostgreSQL (managed or self-hosted)
2. SQLite (local / embedded) — **Recommended**
3. MySQL / MariaDB
4. NoSQL document store (e.g. MongoDB)
5. Other: _______________

Hints:
- Recommended because: single-user / local-first apps usually need zero ops and simple backups.
- To decide: check existing `package.json`, ORM config, or hosting limits.
- Trade-off: SQLite is simple; PostgreSQL scales better for multi-user concurrent writes.
```

## Anti-patterns (MUST NOT)

- Open-ended questions with no options
- More than one primary question per turn (unless deferred)
- Hiding the Recommended marker
- Proceeding after asking without waiting for an answer
- Using the protocol for trivia that does not change the plan
