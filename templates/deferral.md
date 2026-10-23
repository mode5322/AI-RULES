# Deferral Protocol

## Purpose

Strict mode requires clarifying questions and checks **before** execution. The user may defer those checks **for this time only**. Deferral never becomes a standing waiver.

Holding the user’s first request until agent rules are configured is the rules-setup gate in `laws/00-core.md`. That hold is agent-initiated. It is not this deferral. To skip the gate **for the current task only**, use one-time deferral below. To stop the rules-setup question walk until the user later asks to configure the rules, use the fixed pause-protocol phrase (sets `configure-on-request`).

## How the user defers

### One-time deferral (current task only)

The user must clearly say they want to skip questions/checks **once**, for the current task. Fixed acceptable phrasing (do not re-ask for a project-specific list unless the user adds synonyms):

- "Defer for this time only"
- "Skip questions this time only"
- "Proceed without clarifying for this task only"
- "One-time deferral — continue"

Vague phrases like "just do it" or "I don't care" are **not** enough unless they also imply a one-time skip. If ambiguous, ask one confirmation using the question protocol.

### Pause question protocol until rules configuration is requested

A separate fixed phrase switches rules-setup mode to `configure-on-request` (see `laws/00-core.md`). It is **not** a one-time deferral. Fixed title / acceptable phrasing:

- "Stop the question protocol until I ask to configure the rules"
- Arabic title (same meaning): «إيقاف بروتوكول الأسئلة إلى أن أطلب ضبط إعدادات القواعد»

When the user says this (or an exact local synonym recorded under PROJECT-SPECIFIC):

1. Set rules-setup mode to `configure-on-request` in the project profile and in `laws/00-core.md` PROJECT-SPECIFIC.
2. Stop the rules-setup question walk. Do not hold product/code work solely because settings are blank.
3. Resume configuring settings only when the user explicitly asks to configure the rules.
4. Task-level gates that still apply under other laws (security, secrets, data-loss, illegal-request refusals, and clarifying questions required by the current product task) are **not** waived by this phrase.

## Agent behavior when deferred (one-time only)

1. Record that deferral applies **only to the current user request / task**.
2. Proceed with best judgment and state assumptions briefly.
3. Prefer safer defaults; avoid irreversible actions when possible.
4. After the deferred task completes (or is abandoned), restore full strict mode automatically.
5. Do **not** treat prior deferrals as permission for later tasks.
6. Security, data-loss, and illegal-request refusals are **never** deferred.
7. Do **not** treat the pause-protocol phrase above as a one-time deferral; handle it under **Pause question protocol** instead.

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

- Allowed deferral phrases (**fixed pack defaults** — already configured; add local synonyms only if the project needs more):
  - One-time: "Defer for this time only"; "Skip questions this time only"; "Proceed without clarifying for this task only"; "One-time deferral — continue"
  - Pause question protocol until rules configuration is requested (`configure-on-request`): "Stop the question protocol until I ask to configure the rules"; «إيقاف بروتوكول الأسئلة إلى أن أطلب ضبط إعدادات القواعد»
- Roles allowed to defer: _______________
- Actions that must never be deferred: _______________
