# 02 — Discussion (CEO + HR + Sales)

## Purpose

Before executing any **new plan**, force a short multi-angle review so technical work aligns with business, people, and go-to-market realities.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`

Current: _______________

## When this module applies / when to skip

- Applies: any new plan (feature, rewrite, major refactor, launch, pricing-affecting change, hiring-tooling impact, customer-facing flow).
- Skip: trivial typo/format-only changes with no product/plan impact.
- If “is this a new plan?” is unclear, ask once.

## Hard rules (MUST / MUST NOT)

- MUST, for any new plan, briefly discuss from **CEO**, **HR**, and **Sales** angles before implementation.
- MUST keep each angle short (a few sentences): risk, opportunity, people impact, customer impact.
- MUST then ask whether another specialty is needed (legal, finance, support, security, ops, design, etc.).
- MUST NOT treat the discussion as theater — capture decisions that change requirements.
- MUST NOT block forever; after discussion + specialty question, proceed once answers exist (or one-time deferral).
- MUST NOT skip this gate on “small” features that still change user journeys, data, or pricing narratives.

## Angle prompts (use every new plan)

### CEO

- Does this advance the core mission?
- What is the opportunity cost?
- What failure would hurt the company most?

### HR

- Does this change workloads, roles, training, or access for staff?
- Any burnout / process friction risk?
- Any permission or policy implications for employees?

### Sales

- How does this help win, retain, or expand customers?
- What objection does it remove — or create?
- Is the value explainable in one sentence?

## Question protocol

### Example — Specialty add-on

```markdown
### Question
After CEO / HR / Sales review, which extra specialty should join this plan discussion?

1. None — proceed with the three-angle notes — **Recommended**
2. Security / privacy specialist lens
3. Finance / pricing lens
4. Support / operations lens
5. Other: _______________

Hints:
- Recommended when the plan is a normal product iteration without regulated data or pricing changes.
- To decide: regulated data, money movement, or high support load → pick a specialty.
```

### Example — Plan posture

```markdown
### Question
Given the three-angle discussion, how should we proceed?

1. Proceed with the proposed plan as-is — **Recommended**
2. Proceed with a reduced MVP slice
3. Redesign the plan before any coding
4. Pause for stakeholder confirmation outside chat
5. Other: _______________
```

## New-project workflow

1. Draft the plan in one short paragraph.
2. Write CEO / HR / Sales notes.
3. Ask specialty + proceed questions.
4. Update `01-requirements.md` PROJECT-SPECIFIC if the discussion changed scope.
5. Continue to architecture / UI / DB laws.

## Existing-project workflow

1. Frame the remediation or change as a plan (not a pile of patches).
2. Run CEO / HR / Sales angles on customer trust, staff process, and revenue risk.
3. Prefer fixes that protect reputation and support load over flashy rewrites.

## Post-change checklist hooks

- [ ] New plan had CEO/HR/Sales notes (or one-time deferral recorded)
- [ ] Specialty question asked
- [ ] Resulting decisions reflected in requirements/profile

## PROJECT-SPECIFIC

- Company stage: _______________
- CEO priorities: _______________
- HR constraints (roles, training, access): _______________
- Sales motion (self-serve / assisted / B2B): _______________
- Default extra specialties: _______________
- Plans that always require external approval: _______________
