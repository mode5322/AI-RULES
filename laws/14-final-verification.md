# 14 — Final Verification

## Purpose

Define the done-gate before the agent claims work is complete.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`

Current: _______________

## When this module applies / when to skip

- Applies at the end of every implementation task.
- Applies after remediation batches on existing projects.
- Skip only for pure Q&A with no repo changes (still summarize assumptions).

## Hard rules (MUST / MUST NOT)

- MUST NOT claim “done” until acceptance criteria are checked.
- MUST re-run the mandatory five-point review at the end:
  1. Modified elements
  2. DB compatibility
  3. Logic / math
  4. Security / vulns
  5. Quality + structural compatibility
- MUST note what was verified and what was not (honest gaps).
- MUST include evidence from **terminal and/or live** runs when `09-testing.md` applies (commands run, exit codes/logs observed, live steps) — MUST NOT claim final verify from code reading alone.
- MUST confirm question gates were satisfied or one-time deferral was used.
- MUST confirm error fixes waited for user choice when `15-error-handling.md` applied.
- MUST update PROJECT-SPECIFIC blanks if new project truths were learned.
- MUST NOT leave the repo in a knowingly broken state without stating it and proposing next options.

## Question protocol

### Example — Done criteria for this task

```markdown
### Question
What should count as “done” for this task?

1. Acceptance criteria met + five-point review passed — **Recommended**
2. Code complete; tests/docs deferred intentionally
3. Demo-ready only (known gaps listed)
4. Plan delivered; implementation not requested
5. Other: _______________
```

### Example — Residual risk

```markdown
### Question
Residual risks remain. How proceed?

1. Fix residual critical risks before closing — **Recommended**
2. Close with documented follow-ups
3. Add monitoring/logging only for now
4. Revert the change
5. Other: _______________
```

## New-project workflow

1. Re-read acceptance criteria from `01-requirements.md`.
2. Run command and/or live checks agreed in `09-testing.md` (monitor terminal; record evidence).
3. Complete five-point review.
4. Summarize changes, risks, and next steps briefly.
5. Stop — do not expand scope.

## Existing-project workflow

1. Verify fixes against the remediation plan.
2. Confirm compatibility with untouched modules.
3. Ensure no “quick hack” was used where systemic impact exists.
4. Update audit notes in `13-ai-review.md` / profile.

## Post-change checklist hooks

- [ ] Acceptance checked
- [ ] Five-point review done
- [ ] Terminal/live evidence noted per `09-testing.md` (or honest gap stated)
- [ ] Gaps stated
- [ ] PROFILE updated if needed
- [ ] No silent leftover breakage

## PROJECT-SPECIFIC

- Definition of done: _______________
- Mandatory commands before done: _______________
- Release checklist path: _______________
- Stakeholders to notify: _______________
