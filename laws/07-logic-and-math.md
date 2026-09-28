# 07 — Logic and Math

## Purpose

Prevent incorrect business calculations, state machines, and numeric edge cases — especially money, quantities, taxes, and dates.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE` for product apps

Current: _______________

## When this module applies / when to skip

- Applies: pricing, inventory, taxes, discounts, scheduling, permissions math, aggregations, scoring.
- Applies whenever invariants exist (“stock cannot go negative”, “paid ≤ owed”).
- `N/A` only for pure content/docs with no calculations or state rules.

## Hard rules (MUST / MUST NOT)

- MUST NOT use raw binary floating-point for money.
- MUST use integers (minor units), decimal libraries, or the project’s money helpers.
- MUST separate calculation from display/formatting.
- MUST define rounding rules explicitly (half-up, banker’s, per-locale).
- MUST encode invariants in service/domain logic, not only in UI.
- MUST handle zero, negative, empty, and overflow cases intentionally.
- MUST NOT “patch” a wrong total by hardcoding exceptions without fixing the formula.
- After changes: MUST re-check logic/math as part of mandatory review.

## Question protocol

### Example — Money representation

```markdown
### Question
How should money amounts be stored and computed?

1. Integer minor units (e.g. cents) — **Recommended**
2. Decimal type / library with fixed scale
3. Floating-point numbers
4. Strings of decimal text only
5. Other: _______________

Hints:
- Avoid option 3 for anything financial.
- To decide: check existing helpers like `currencyMath` / `addMoney`.
```

### Example — Rounding

```markdown
### Question
Which rounding rule applies to currency calculations?

1. Round half up to currency scale — **Recommended**
2. Round half even (banker’s rounding)
3. Always floor / always ceil (explain where)
4. Jurisdiction-specific tax rounding rules (document)
5. Other: _______________
```

### Example — Invariant ownership

```markdown
### Question
Where should critical invariants be enforced?

1. Domain/service layer with DB constraints as backup — **Recommended**
2. UI only
3. Database triggers only
4. Report/export layer only
5. Other: _______________
```

## New-project workflow

1. List calculations and invariants early.
2. Choose money/numeric representation.
3. Implement shared helpers; reuse them everywhere.
4. Add examples of expected inputs/outputs in PROJECT-SPECIFIC.
5. Verify edge cases before calling work done.

## Existing-project workflow

1. Find existing math helpers and follow them.
2. If multiple conflicting methods exist, plan consolidation — don’t add a third.
3. Fix root formulas; avoid one-off corrections in callers.
4. Recompute sample fixtures after changes.

## Post-change checklist hooks

- [ ] Money/precision approach correct
- [ ] Rounding explicit
- [ ] Invariants held on edge cases
- [ ] Display vs calculation separated

## PROJECT-SPECIFIC

- Money helper path: _______________
- Currency list: _______________
- Rounding rule: _______________
- Tax rules summary: _______________
- Critical invariants: _______________
- Known formula docs: _______________
