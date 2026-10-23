# 02 — Discussion (Sales)

## Purpose

When a new plan changes pricing or who the product is for, write a short customer note before implementation.

## Status

`ACTIVE` when the plan changes pricing or the audience. Otherwise skip this file.

## When this module applies / when to skip

- Applies: a pricing change, or a change to who the product is for.
- Skip: every other task, including typo, format, refactor, and staff-process work.

## Hard rules (MUST / MUST NOT)

- Use the **Sales** angle only when the plan changes pricing or who the product is for.
- Keep the note to one or two sentences.
- Do not ask for another specialty unless the user asks.
- Do not block the task when the plan does not change pricing or the audience.

## Angle prompts (only when this gate applies)

### Sales

- How does this help win, retain, or expand customers?
- What objection does it remove — or create?
- Is the value explainable in one sentence?

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Draft the plan in one short paragraph.
2. Write the Sales note only when the plan changes pricing or who the product is for.
3. Do not ask for another specialty unless the user asks.
4. Do not write a second requirements list.
5. Continue the task. Do not open architecture, UI, or database questions the task does not need.

## Existing-project workflow

1. Frame the remediation or change as a plan (not a pile of patches).
2. Use the Sales angle only when the change affects customers or revenue.
3. Prefer fixes that protect reputation and support load over flashy rewrites.

## Post-change checklist hooks

- [ ] The Sales note was used only when pricing or the audience changed
- [ ] No extra specialty question was asked
- [ ] No second requirements list was written

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
