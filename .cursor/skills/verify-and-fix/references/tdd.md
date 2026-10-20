# Red-green-refactor (adapted from the tdd pattern)

Use when the project has a test runner or the user wants tests.

1. Pick ONE small vertical slice of behavior.
2. RED: write a test that describes the behavior through the public interface. Run it; it must fail for the right reason.
3. GREEN: write the minimum code to pass. Run it.
4. REFACTOR: clean up with tests green.
5. Repeat for the next slice.

Good tests check behavior, not implementation details. Do not mock what you own without a reason.
If no test runner exists, do not install one without asking.
