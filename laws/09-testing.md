# 09 — Testing

## Purpose

Define when and how to verify behavior so changes do not ship on hope alone.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`

Current: _______________

## When this module applies / when to skip

- Applies: logic, API, data, and critical UI flows.
- Do not add large test suites unprompted if the project rule is minimal — but MUST still verify acceptance criteria.
- `N/A` only when the consuming project explicitly forbids automated tests **and** manual verification is defined.
- Security scanners (dependency audit, secrets, Semgrep, ZAP baseline, platform checklists) are **not** functional tests — see `18-security-tooling.md` and `10-security.md`. Do not count a green security scan as acceptance-criteria verification, or a passing unit suite as a security review.

## Hard rules (MUST / MUST NOT)

- MUST verify acceptance criteria before claiming done.
- MUST prefer tests at the layer that catches the bug cheapest (unit for pure logic; integration for DB/API).
- MUST NOT claim “tested” without saying what was run.
- MUST NOT add brittle UI snapshot spam unless the project uses that pattern.
- MUST test money/invariant edge cases when those modules are touched.
- MUST update or remove obsolete tests when behavior intentionally changes.
- If test strategy is unclear before build/start, ask.

## Question protocol

### Example — Verification level for this task

```markdown
### Question
What verification is required before we call this done?

1. Focused automated tests for changed logic + manual happy path — **Recommended**
2. Manual verification only
3. Full suite run in CI locally
4. Write tests first (TDD) for this change
5. Other: _______________
```

### Example — Test tooling

```markdown
### Question
Which test runner/stack should we use?

1. Whatever the repo already uses — **Recommended**
2. Add a standard unit test runner for the language
3. API/integration tests only
4. End-to-end browser tests only
5. Other: _______________
```

## New-project workflow

1. Choose test stack early if quality bar requires it.
2. Put pure logic in testable modules.
3. Add fixtures for money/date edge cases.
4. Document how to run tests in PROJECT-SPECIFIC.
5. Gate merges on the agreed checks.

## Existing-project workflow

1. Detect existing test commands and patterns.
2. Extend them; don’t introduce a second framework without approval.
3. When fixing bugs, add a regression check when the project’s bar allows.
4. If tests are absent, propose a minimal harness as part of remediation planning.

## Post-change checklist hooks

- [ ] Acceptance criteria checked
- [ ] Relevant tests run or manual steps recorded
- [ ] Edge cases for math/validation considered
- [ ] CI impact understood

## PROJECT-SPECIFIC

- Test runner: _______________
- Commands: _______________
- Required checks before done: _______________
- Coverage expectations: _______________
- Flaky test policy: _______________
