# Root-cause diagnosing loop

Goal: fix the cause, not the symptom. No fix before step 1 and step 4 are done.

1. **Reproduce.** Get a command, test or click-path that fails reliably.
2. **Minimise.** Remove everything not needed to trigger the failure.
3. **Hypothesise.** Write 2-3 possible causes, most likely first.
4. **Prove the cause.** Instrument one hypothesis at a time (temporary logs, checks, debugger) until one is confirmed with evidence. Then ask "why?" again on the confirmed cause until reaching the origin (where the bad value, state or design decision first appears). Stop only when a deeper "why" has no code-level answer.
5. **Write the root-cause note** (2 sentences): the root cause, and the evidence that proves it. If you cannot write it, you are guessing: go back to step 4.
6. **Fix the origin.** Forbidden patches that only hide the symptom: swallowing errors with try/catch, adding a default value that masks bad data, `setTimeout` or retries to hide timing bugs, disabling a failing check or test, special-casing the failing input.
7. **Hunt siblings.** Search the codebase for the same pattern. Fix the ones in scope of this task; list the rest for the user.
8. **Regression test.** Add a test (or documented manual step) that fails without the fix.
9. **Close the door.** Ask: can a type, validation, constraint or design change make this bug impossible? Propose it; do not implement it without the user's approval.
10. **Clean up** temporary logs. Re-run all checks.
