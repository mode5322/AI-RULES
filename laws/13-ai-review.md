# 13 — AI Review

## Purpose

Define how the agent reviews its own work and how it audits **existing** projects when AI is introduced later.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`

Current: _______________

## When this module applies / when to skip

- Applies after every change (self-review).
- Applies when asked to review, audit, harden, or “fix the project.”
- Applies strongly for existing-project onboarding (with `16-existing-projects.md`).
- Skip only when the user explicitly wants an uninterrupted brainstorm and used one-time deferral.

## Hard rules (MUST / MUST NOT)

- MUST self-review every change against:
  1. Modified elements (what changed and why)
  2. DB compatibility
  3. Logic / math
  4. Security / vulnerabilities
  5. Quality + structural compatibility
- MUST be defect-first: prioritize correctness, data loss, security, and breakage over style nits.
- MUST NOT claim a review without listing what was checked.
- MUST NOT “fix forward” by stacking patches without a rethink when systemic issues appear.
- For existing projects: MUST follow review → rethink → issue plan → fixes (see also `16-existing-projects.md`).
- MUST wait for user direction when multiple remediation strategies exist (question protocol).
- Prefer root-cause remediation; allow quick fix only if impact is isolated.

## Existing-project audit / remediation flow

1. **Inventory** — stack, entrypoints, architecture reality, DB, auth, critical user journeys.
2. **Review** — defects, smells, inconsistencies, security holes, broken invariants.
3. **Rethink** — which issues are symptoms vs root causes; what compatibility constraints exist.
4. **Plan** — ordered issue list with severity; proposed fixes; CEO/HR/Sales brief if it’s a new plan (`02-discussion.md`).
5. **Confirm** — question protocol on approach (quick vs root-cause; sequencing).
6. **Fix** — implement approved items; self-review after each unit.
7. **Verify** — `14-final-verification.md` + update PROJECT-SPECIFIC with discovered truths.

## Question protocol

### Example — Review depth

```markdown
### Question
What depth of AI review do you want?

1. Critical issues only (data loss, security, crashes, broken money) — **Recommended**
2. Critical + major maintainability risks
3. Full audit including style/consistency
4. Diff-only review of current uncommitted changes
5. Other: _______________
```

### Example — Remediation approach

```markdown
### Question
How should we remediate the findings?

1. Root-cause fixes in priority order, compatibility-preserving — **Recommended**
2. Quick isolated fixes first; schedule systemic work
3. Written plan only; no code yet
4. Stop after top N critical issues (specify N in custom)
5. Other: _______________
```

## New-project workflow

1. After each implementation unit, run the five-point review.
2. Fix defects found before expanding scope.
3. Record recurring risks in PROJECT-SPECIFIC.

## Existing-project workflow

1. Do not start feature work until audit posture is agreed (unless deferred once).
2. Execute the audit/remediation flow above.
3. Cross-link findings to `15-error-handling.md` when runtime errors appear.
4. Keep the public origin template blank; write findings only in the consuming project.

## Post-change checklist hooks

- [ ] Five-point review completed
- [ ] Findings reported honestly
- [ ] Remediation strategy confirmed when multiple options exist
- [ ] PROFILE / PROJECT-SPECIFIC updated after audits

## PROJECT-SPECIFIC

- Last audit date: _______________
- Review depth default: _______________
- Open critical findings: _______________
- Remediation backlog path: _______________
- Compatibility constraints discovered: _______________
