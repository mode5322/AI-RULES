# 05 — Architecture

## Purpose

Keep structure intentional: clear layers, naming, and boundaries so features stay maintainable.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`

Current: _______________

## When this module applies / when to skip

- Applies: new modules, refactors, cross-cutting changes, bootstrap of folder layout.
- Lightweight apply: small fixes must still respect existing boundaries.
- `N/A` only for docs-only / non-code chores.

## Hard rules (MUST / MUST NOT)

- MUST read surrounding structure before adding files.
- MUST follow the project’s chosen layout once PROFILE is filled.
- MUST keep layer boundaries (e.g. screens compose; services orchestrate; database access isolated; utils stay pure) when that model is adopted.
- MUST NOT place business rules only in UI controls.
- MUST NOT introduce a second parallel architecture style without an explicit decision.
- MUST prefer extending existing modules over creating near-duplicates.
- MUST keep the change small; no speculative frameworks.
- Before build/start, MUST clarify architecture when unknown.

### Suggested default layout (adapt to stack)

```
screens/      # page-level UI
components/   # reusable UI (group by screen/service when needed)
services/     # business orchestration + exports barrel
utils/        # pure helpers
database/     # schema + data access API
types/        # shared types
hooks/        # reusable hooks if applicable
```

Adapt names to the stack (e.g. `app/`, `src/`, `lib/`) but keep role clarity.

## Question protocol

### Example — Architecture style

```markdown
### Question
Which architecture style should this project follow?

1. Layered (screens → services → database) — **Recommended**
2. Feature folders (vertical slices)
3. Framework default (e.g. Next.js app router conventions only)
4. Hexagonal / ports-and-adapters
5. Other: _______________

Hints:
- Recommended for business apps with clear UI vs domain vs data needs.
- To decide: inspect current folders; don’t fight a mature existing layout.
```

### Example — Where business rules live

```markdown
### Question
Where must authorization and business validation run?

1. Service layer (UI may pre-check but never solely) — **Recommended**
2. UI only
3. Database constraints only
4. API gateway / middleware only
5. Other: _______________
```

## New-project workflow

1. Choose architecture style via questions.
2. Create skeleton folders matching the decision.
3. Define naming conventions in PROJECT-SPECIFIC.
4. Add services barrel / public entrypoints if applicable.
5. Implement features inside the agreed boundaries.

## Existing-project workflow

1. Map the real architecture (not the aspirational one).
2. New code MUST match the dominant real pattern unless a migration plan exists.
3. If patterns conflict, propose a compatibility-preserving consolidation plan (see `16-existing-projects.md`).
4. Do not “fix” structure with a wide rewrite unless approved.

## Post-change checklist hooks

- [ ] Files landed in the correct layer/folder
- [ ] No boundary violations (UI bypassing services, etc.)
- [ ] Naming matches conventions
- [ ] No duplicate module introduced

## PROJECT-SPECIFIC

- Architecture style: _______________
- Root source folder: _______________
- Layer map: _______________
- Naming rules: _______________
- Services export path: _______________
- Forbidden imports: _______________
- Monorepo packages: _______________
