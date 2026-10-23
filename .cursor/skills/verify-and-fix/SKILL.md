---
name: verify-and-fix
description: Use after finishing any feature, fix or update, and whenever something fails. Verifies manually (build, lint, tests, run), then with available MCP tools (browser), fixes errors with a disciplined loop (max 3 attempts), reviews the diff, and reports honestly what was and was not verified.
---

# Verify and fix

## Workflow
1. **Manual checks.** Detect build, lint, test, and run commands from the repo (`package.json` scripts, `composer.json`, `pubspec.yaml`, or the README). Run what exists: typecheck, lint, build, tests, start. Do not ask for those commands.
2. **MCP checks.** List the tools actually available. If a browser/automation tool exists, open the app, exercise the new feature, check console errors and failed network requests. If none exists, say so; do not claim UI verification.
3. **Fix loop.** For each failure follow `references/diagnosing.md`. If the project has a test setup, or the user asked for tests, follow `references/tdd.md` for the regression test.
   - Before any second attempt, write the root-cause note (cause + evidence) from `references/diagnosing.md`. No new attempt without it.
   - Maximum 3 fix attempts per issue.
   - After 3 failures stop. Show: the error, what was tried, and up to 3 options. Wait for the user's choice.
4. **Review.** Follow `references/review.md` on the diff. If UI changed, also run the UI audit there.
5. **Report** in the user's language: passed / failed / not verified, files changed, and anything left open.

## Rules
- Re-run all checks after every fix.
- Never mark something verified that was not actually run.
- Do not widen scope while fixing: only touch what the failure needs.
