# 01 — Requirements

## Purpose

Force clear, testable requirements before implementation so the agent does not invent scope or ship the wrong product.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default while undecided: `PROJECT-SPECIFIC`

Current: _______________

## When this module applies / when to skip

- Applies: any new feature, new project bootstrap, behavior change, or API contract change.
- Skip only when marked `N/A` for non-product chores (e.g. typo in README) **and** the change cannot alter behavior.
- If unsure whether requirements are needed, ask — do not assume.

## Hard rules (MUST / MUST NOT)

- MUST gather goals, users, constraints, success criteria, and non-goals before build/start.
- MUST NOT start coding while critical requirements are unknown (unless one-time deferral).
- MUST translate requirements into acceptance checks the agent can verify later.
- MUST prefer measurable outcomes over vague adjectives (“fast”, “nice”, “modern”).
- MUST record confirmed requirements in PROJECT-SPECIFIC / project profile.
- MUST NOT expand scope beyond agreed requirements without a new question gate.
- During/after build: ask only when requirements become ambiguous.

## Question protocol

Follow `templates/question-protocol.md`.

### Example — Primary outcome

```markdown
### Question
What is the primary outcome for this work?

1. Ship a usable MVP slice end-to-end — **Recommended**
2. Design/architecture only (no implementation yet)
3. Fix/stabilize an existing broken behavior
4. Explore options and recommend; wait for a second approval to build
5. Other: _______________

Hints:
- Recommended when the user wants working software soon with controlled scope.
- To decide: check whether screens/APIs already exist and whether a deadline was stated.
```

### Example — Success criteria

```markdown
### Question
How will we know this is done?

1. User can complete the main happy path manually
2. Automated tests cover the agreed acceptance cases — **Recommended**
3. Demo checklist signed off by stakeholder
4. Performance/security gate passed in addition to functional checks
5. Other: _______________
```

### Example — Non-goals

```markdown
### Question
What should explicitly be out of scope for this pass?

1. No new integrations / third-party services — **Recommended**
2. No UI redesign; logic-only
3. No database schema changes
4. No auth/roles changes
5. Other: _______________
```

## New-project workflow

1. Identify problem, users, platforms, and constraints.
2. Ask blocking requirement questions (one at a time).
3. Write short acceptance criteria.
4. Hand off to `02-discussion.md` before architecture/UI build.
5. Freeze v1 scope; changes require a new mini-requirements pass.

## Existing-project workflow

1. Reconstruct intended vs actual behavior from code and docs.
2. Ask which discrepancies are bugs vs intentional drift.
3. Define remediation requirements before coding (see `16-existing-projects.md`).
4. Avoid “fixing” behavior that product actually wants.

## Post-change checklist hooks

- [ ] Change maps to an agreed requirement
- [ ] Acceptance criteria still valid
- [ ] No silent scope creep
- [ ] PROJECT-SPECIFIC requirements updated if decisions changed

## PROJECT-SPECIFIC

- Problem statement: _______________
- Primary users: _______________
- Platforms: _______________
- Must-have (v1): _______________
- Nice-to-have (later): _______________
- Non-goals: _______________
- Acceptance criteria: _______________
- Constraints (time, budget, compliance, hosting): _______________
- Stakeholders / approvers: _______________
