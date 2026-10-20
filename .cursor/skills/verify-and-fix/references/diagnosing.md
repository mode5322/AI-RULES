# Diagnosing loop (adapted from the diagnosing-bugs pattern)

1. **Reproduce.** Get a command, test or click-path that fails reliably. No fix before this.
2. **Minimise.** Remove everything not needed to trigger the failure.
3. **Hypothesise.** Write 2-3 possible causes, most likely first.
4. **Instrument.** Add temporary logs or checks to confirm or reject one hypothesis at a time.
5. **Fix** the confirmed cause, not the symptom.
6. **Regression test.** Add a test or a documented manual step that fails without the fix.
7. **Clean up** temporary logs. Re-run all checks.
