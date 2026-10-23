# 14 — Final Verification

## Purpose

Define the done-gate before the agent claims work is complete.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`


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
- MUST update the project profile when a Behavior or System design fact was learned. Do not add a blank in this file.
- MUST NOT leave the repo in a knowingly broken state without stating it and proposing next options.

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

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

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
