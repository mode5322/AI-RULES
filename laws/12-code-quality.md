# 12 — Code Quality

## Purpose

Keep code readable, consistent, and maintainable without gold-plating.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`

Current: _______________

## When this module applies / when to skip

- Applies to all code changes.
- Depth scales with risk; still no sloppy shared-module edits.

## Hard rules (MUST / MUST NOT)

- MUST match existing naming, formatting, and abstractions.
- MUST reuse existing helpers/components instead of reimplementing.
- MUST keep functions focused; avoid huge catch-all modules for new code.
- MUST NOT over-engineer: no extra layers “for the future.”
- MUST NOT add unsolicited docs, comments, or refactors.
- Comment only non-obvious business logic.
- MUST delete dead code introduced by the change when safe.
- MUST keep types accurate when the project is typed.
- After changes: include quality + structural compatibility in mandatory review.

## Question protocol

### Example — Quality bar for this task

```markdown
### Question
What quality bar should we apply?

1. Match surrounding code; fix only what we touch — **Recommended**
2. Opportunistic cleanup in the same files if low risk
3. Broader refactor of the module
4. Strict lint/type clean for the whole package
5. Other: _______________
```

### Example — Duplication

```markdown
### Question
We found duplicated logic. What should we do?

1. Extract a shared helper now if ≥2 call sites and stable behavior — **Recommended**
2. Leave duplication for this pass; note follow-up
3. Rewrite all call sites to a new abstraction
4. Keep copies intentional (document why)
5. Other: _______________
```

## New-project workflow

1. Establish formatter/linter early if the stack expects it.
2. Write boring, clear code.
3. Create shared helpers only when reuse is real.
4. Record conventions in PROJECT-SPECIFIC.

## Existing-project workflow

1. Mirror local style even if you prefer another.
2. Don’t reformat unrelated files.
3. Quality issues project-wide go into the remediation plan, not drive-by rewrites.

## Post-change checklist hooks

- [ ] Style matches neighbors
- [ ] No speculative abstractions
- [ ] Types/lint clean for touched scope (as project requires)
- [ ] Structural compatibility OK

## PROJECT-SPECIFIC

- Formatter / linter: _______________
- Naming conventions: _______________
- Max complexity preferences: _______________
- Comment policy: _______________
- Forbidden patterns: _______________
