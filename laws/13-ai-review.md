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

### Over-engineering review (complexity-only pass)

When the user asks to review for bloat/over-engineering, or when a review depth includes maintainability:

- MUST hunt only unnecessary complexity (not a substitute for correctness/security review).
- Prefer one-line findings: location, tag, what to cut, replacement.
- Tags:
  - `delete:` dead code, unused flexibility, speculative feature
  - `stdlib:` reinvented standard library — name the equivalent
  - `native:` reinvented platform feature — name the feature
  - `yagni:` one-implementation abstraction, unused config, single-caller layer
  - `shrink:` same logic, fewer lines — show shorter form
- MUST NOT apply mass deletions without question protocol / user approval.
- Correctness, security, and data-loss issues remain defect-first and outrank complexity nits.

### Simplification debt ledger

When asked for deferred-shortcut debt, or during existing-project audits:

- Scan for markers from `12-code-quality.md` (`simplify:` / `ponytail:` / PROJECT-SPECIFIC prefix).
- Report: file:line — what was simplified — ceiling — upgrade trigger.
- Tag `no-trigger` when a marker lacks an upgrade path.
- Report only; MUST NOT change code until the user chooses a remediation approach.

## Existing-project audit / remediation flow

1. **Inventory** — stack, entrypoints, architecture reality, DB, auth, critical user journeys.
2. **Review** — defects, smells, inconsistencies, security holes, broken invariants; optionally a complexity pass (tags above).
3. **Rethink** — which issues are symptoms vs root causes; what compatibility constraints exist.
4. **Plan** — ordered issue list with severity; proposed fixes; CEO/HR/Sales brief if it’s a new plan (`02-discussion.md`).
5. **Confirm** — question protocol on approach (quick vs root-cause; sequencing).
6. **Fix** — implement approved items; self-review after each unit; apply `12` ladder to new code.
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

### Example — Complexity review scope

```markdown
### Question
Should this review include an over-engineering / bloat pass?

1. Yes — diff-only complexity tags (delete/stdlib/native/yagni/shrink) — **Recommended** when reviewing a change
2. Yes — whole-repo complexity audit (ranked)
3. No — correctness/security only this time
4. Debt ledger only (simplification markers)
5. Other: _______________
```

## New-project workflow

1. After each implementation unit, run the five-point review.
2. Fix defects found before expanding scope.
3. Optionally run a short complexity pass on the diff when the change grew large.
4. Record recurring risks in PROJECT-SPECIFIC.

## Existing-project workflow

1. Do not start feature work until audit posture is agreed (unless deferred once).
2. Execute the audit/remediation flow above.
3. Offer whole-repo complexity audit and/or debt ledger when bloat is suspected.
4. Cross-link findings to `15-error-handling.md` when runtime errors appear.
5. Keep the public origin template blank; write findings only in the consuming project.

## Post-change checklist hooks

- [ ] Five-point review completed
- [ ] Complexity tags listed when a bloat pass was requested/needed
- [ ] Findings reported honestly
- [ ] Remediation strategy confirmed when multiple options exist
- [ ] PROFILE / PROJECT-SPECIFIC updated after audits

## PROJECT-SPECIFIC

- Last audit date: _______________
- Review depth default: _______________
- Include complexity pass by default?: _______________
- Open critical findings: _______________
- Remediation backlog path: _______________
- Simplification debt ledger path: _______________
- Compatibility constraints discovered: _______________
