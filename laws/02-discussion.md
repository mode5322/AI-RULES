# 02 — Discussion (CEO + HR + Sales)

## Purpose

Before executing any **new plan**, force a short multi-angle review so technical work aligns with business, people, and go-to-market realities.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`


## When this module applies / when to skip

- Applies: any new plan (feature, rewrite, major refactor, launch, pricing-affecting change, hiring-tooling impact, customer-facing flow).
- Skip: trivial typo/format-only changes with no product/plan impact.
- If “is this a new plan?” is unclear, ask once.

## Hard rules (MUST / MUST NOT)

- Use the **CEO**, **HR**, and **Sales** angles only when a new plan changes pricing, staff work, or who the product is for.
- Keep each angle to one or two sentences.
- Do not ask for another specialty unless the user asks, or the plan changes pricing, staff work, or regulated data.
- Capture a decision only when it changes the current request.
- Do not block the task on this discussion when the plan does not change those things.

## Angle prompts (only when this gate applies)

### CEO

- Does this advance the core mission?
- What is the opportunity cost?
- What failure would hurt the company most?

### HR

- Does this change workloads, roles, training, or access for staff?
- Any burnout / process friction risk?
- Any permission or policy implications for employees?

### Sales

- How does this help win, retain, or expand customers?
- What objection does it remove — or create?
- Is the value explainable in one sentence?

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Draft the plan in one short paragraph.
2. Write the CEO, HR, and Sales notes only when the plan changes pricing, staff work, or who the product is for.
3. Do not ask for another specialty unless the user asks.
4. Do not write a second requirements list.
5. Continue the task. Do not open architecture, UI, or database questions the task does not need.

## Existing-project workflow

1. Frame the remediation or change as a plan (not a pile of patches).
2. Use the CEO, HR, and Sales angles only when the change affects customers, staff process, or revenue.
3. Prefer fixes that protect reputation and support load over flashy rewrites.

## Post-change checklist hooks

- [ ] Angles were used only when pricing, staff work, or the audience changed
- [ ] No extra specialty question was asked
- [ ] No second requirements list was written

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
