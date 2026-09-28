# 09 — Testing

## Purpose

Define when and how to verify behavior so changes do not ship on hope alone. Scoped tests of a changed or relevant part MUST use real commands and/or live runtime exercise, with terminal monitoring so failures are identified accurately.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`

Current: _______________

## When this module applies / when to skip

- Applies: logic, API, data, and critical UI flows; any scoped test of a changed or relevant part.
- Do not add large test suites unprompted if the project rule is minimal — but MUST still verify acceptance criteria via commands and/or live exercise.
- `N/A` only when the consuming project explicitly forbids automated tests **and** live/manual verification is defined in PROJECT-SPECIFIC (still command-or-live, not theory-only).
- Security scanners (dependency audit, secrets, Semgrep, ZAP baseline, platform checklists) are **not** functional tests — see `18-security-tooling.md` and `10-security.md`. Do not count a green security scan as acceptance-criteria verification, or a passing unit suite as a security review.

## Hard rules (MUST / MUST NOT)

### Command / live proof (mandatory for scoped tests)

- MUST verify acceptance criteria before claiming done.
- For any **scoped test** of a changed or relevant part, MUST run **real commands** and/or **live runtime exercise** (app, server, device, emulator, or equivalent as applicable) — not theory-only reasoning.
- MUST NOT claim “tested” based only on reading code, static review, or imagined outcomes.
- MUST NOT claim “tested” without saying **what was run** (command(s), live steps) and **what was observed**.

### Terminal monitoring

- While commands or live runs are in progress, MUST **monitor the terminal** (stdout, stderr, exit codes, and relevant logs) to understand what is happening.
- On failure or anomaly: MUST **capture what happened** → identify the **likely problem** → present **solution step(s)** using the standard error protocol in `15-error-handling.md` (4 solutions + custom blank + one **Recommended**; wait for user choice).
- MUST NOT silently ignore failing exit codes, stack traces, or repeated warnings that indicate the scoped feature is broken.

### Layer and quality

- MUST prefer tests at the layer that catches the bug cheapest (unit for pure logic; integration for DB/API; live for end-to-end flows).
- MUST NOT add brittle UI snapshot spam unless the project uses that pattern.
- MUST test money/invariant edge cases when those modules are touched.
- MUST update or remove obsolete tests when behavior intentionally changes.
- If test strategy or live-proof method is unclear before build/start, ask.

### Stack-adaptive guidance (high-level)

Adapt to the project type; fill PROJECT-SPECIFIC with the concrete commands used here:

| Project type | Typical command / live proof | What to monitor |
|---|---|---|
| Web (frontend/API) | Dev/server start + `curl`/HTTP checks and/or browser exercise of the changed flow | Server/terminal logs, HTTP status, browser console if used |
| Node / CLI | Project test runner + invoke the changed CLI/API path | stdout/stderr, exit code |
| Flutter / mobile | `flutter test` and/or `flutter run` (device/emulator) for the changed feature | Build output, device/logcat-style logs, runtime exceptions |
| Desktop / other | Project’s run + targeted exercise of the changed surface | Process output, crash logs |

Use the repo’s existing scripts when present; do not invent a second stack without approval.

## Question protocol

### Example — Verification level for this task

```markdown
### Question
What verification is required before we call this done?

1. Focused automated tests for changed logic + live/command happy path — **Recommended**
2. Live/manual exercise only (commands + terminal monitoring)
3. Full suite run locally (CI-equivalent) + scoped live check
4. Write tests first (TDD) for this change, then live/command proof
5. Other: _______________

Hints:
- Recommended balances cheap automated coverage with real runtime proof.
- Theory-only or “I read the code” is never enough for a scoped feature test.
```

### Example — Test tooling

```markdown
### Question
Which test runner/stack should we use?

1. Whatever the repo already uses — **Recommended**
2. Add a standard unit test runner for the language
3. API/integration tests only
4. End-to-end browser/device tests only
5. Other: _______________
```

### Example — Live proof method

```markdown
### Question
How should we live-exercise this change?

1. Start the project’s normal run target and exercise the changed flow — **Recommended**
2. Automated tests only (still monitor terminal); no interactive UI
3. HTTP/curl against a running local server
4. Device/emulator run with log monitoring
5. Other: _______________
```

## New-project workflow

1. Choose test stack early if quality bar requires it.
2. Put pure logic in testable modules.
3. Add fixtures for money/date edge cases.
4. Document preferred **test commands** and **how live test is done** in PROJECT-SPECIFIC.
5. Gate merges on the agreed checks — each scoped verification MUST include command and/or live proof with terminal monitoring.
6. On first failure during proof: capture terminal evidence → `15-error-handling.md` options → wait.

## Existing-project workflow

1. Detect existing test commands, run scripts, and live-debug patterns.
2. Extend them; don’t introduce a second framework without approval.
3. When fixing bugs, add a regression check when the project’s bar allows — then re-run command/live proof and monitor the terminal.
4. If tests are absent, propose a minimal harness as part of remediation planning; until then, live/command verification with terminal monitoring remains mandatory for scoped changes.
5. Record discovered run/test commands in PROJECT-SPECIFIC.

## Post-change checklist hooks

- [ ] Acceptance criteria checked
- [ ] Scoped change verified via real commands and/or live exercise (not code-read alone)
- [ ] Terminal monitored (stdout/stderr/exit codes/logs) during the run
- [ ] On failure: evidence captured → problem identified → solutions via `15-error-handling.md`
- [ ] Relevant automated tests run or live steps recorded (what + outcome)
- [ ] Edge cases for math/validation considered
- [ ] CI impact understood

## PROJECT-SPECIFIC

- Test runner: _______________
- Preferred test commands: _______________
- How live test is done (app/server/device steps): _______________
- Terminal / log locations to watch: _______________
- Required checks before done: _______________
- Coverage expectations: _______________
- Flaky test policy: _______________
