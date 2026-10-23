# 07 — Logic and Math

## Purpose

Prevent incorrect business calculations, state machines, and numeric edge cases — especially money, quantities, taxes, and dates.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE` for product apps


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

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. List calculations and invariants early.
2. Choose money/numeric representation.
3. Implement shared helpers; reuse them everywhere.
4. Check the edge values in the change. Do not add a settings blank.
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

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
