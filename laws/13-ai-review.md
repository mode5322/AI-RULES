# 13 — AI Review

## Purpose

Define how the agent reviews its own work and how it audits **existing** projects when AI is introduced later.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`


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
4. **Plan** — ordered issue list with severity; proposed fixes; Sales note only when the plan changes pricing or who the product is for (`02-discussion.md`).
5. **Confirm** — question protocol on approach (quick vs root-cause; sequencing).
6. **Fix** — implement approved items; self-review after each unit; apply `12` ladder to new code.
7. **Verify** — `14-final-verification.md`. Do not add a settings blank.

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. After each implementation unit, run the five-point review.
2. Fix defects found before expanding scope.
3. Optionally run a short complexity pass on the diff when the change grew large.
4. State a recurring risk in the reply. Do not add a settings blank.

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
- [ ] No new settings blank was added

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
