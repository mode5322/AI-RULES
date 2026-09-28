# Deferral Protocol

## Purpose

Strict mode requires clarifying questions and checks **before** execution. The user may defer those checks **for this time only**. Deferral never becomes a standing waiver.

## How the user defers

The user must clearly say they want to skip questions/checks **once**, for the current task. Acceptable phrasing includes:

- "Defer for this time only"
- "Skip questions this time only"
- "Proceed without clarifying for this task only"
- "One-time deferral — continue"

Vague phrases like "just do it" or "I don't care" are **not** enough unless they also imply a one-time skip. If ambiguous, ask one confirmation using the question protocol.

## Agent behavior when deferred

1. Record that deferral applies **only to the current user request / task**.
2. Proceed with best judgment and state assumptions briefly.
3. Prefer safer defaults; avoid irreversible actions when possible.
4. After the deferred task completes (or is abandoned), restore full strict mode automatically.
5. Do **not** treat prior deferrals as permission for later tasks.
6. Security, data-loss, and illegal-request refusals are **never** deferred.

## Confirmation template (if deferral is unclear)

```markdown
### Question
Do you want a one-time deferral of clarifying questions for this task only?

1. Yes — defer questions for this task only, then restore strict mode — **Recommended**
2. No — keep asking required questions before work
3. Defer only non-blocking questions; still ask blocking ones
4. Pause — I will answer questions now
5. Other: _______________
```

## PROJECT-SPECIFIC

- Allowed deferral phrases (add local synonyms): _______________
- Roles allowed to defer: _______________
- Actions that must never be deferred: _______________
