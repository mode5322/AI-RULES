# 01 — Requirements

## Purpose

Force clear, testable requirements before implementation so the agent does not invent scope or ship the wrong product.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default while undecided: `PROJECT-SPECIFIC`


## When this module applies / when to skip

- Applies: any new feature, new project bootstrap, behavior change, or API contract change.
- Skip only when marked `N/A` for non-product chores (e.g. typo in README) **and** the change cannot alter behavior.
- If unsure whether this task changes behavior, read the request again. Do not open a requirements questionnaire for a chore that cannot change behavior.

## Hard rules (MUST / MUST NOT)

- If the user's request already names the outcome, treat that as the requirement. Ask one question only when the outcome is missing and the work cannot start.
- MUST NOT start coding while the outcome of this task is unknown (unless one-time deferral).
- MUST translate that outcome into an acceptance check the agent can verify later.
- MUST prefer measurable outcomes over vague adjectives (“fast”, “nice”, “modern”).
- Record a confirmed product fact in the project profile only when it is a Behavior or System design field.
- MUST NOT expand scope beyond the current request without the user asking for the extra scope.
- For complex requests after gates: MAY ship the minimum that satisfies the request and, in the same response, ask whether the fuller variant is required (see `12-code-quality.md` intensity). MUST NOT silently drop what the user asked for.

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

0. Rules-setup gate in `00-core.md` runs first when a relevant setting is unconfigured. This file is not a setup section.
1. Use the outcome named in the request.
2. Ask one question only when that outcome is missing.
3. Write one acceptance check.
4. Use `02-discussion.md` only when the plan changes pricing, staff work, or who the product is for.
5. Do not add scope the user did not ask for.

## Existing-project workflow

0. Rules-setup gate in `00-core.md` runs first when setup is incomplete. Facts the code already shows are written in that walk.
1. Reconstruct intended vs actual behavior from code and docs.
2. Treat a discrepancy as a bug only when the current request says that behavior is wrong. Do not ask a drift questionnaire otherwise.
3. Define remediation requirements before coding (see `16-existing-projects.md`).
4. Avoid “fixing” behavior that product actually wants.

## Post-change checklist hooks

- [ ] Change maps to the current request
- [ ] Acceptance check still valid
- [ ] No silent scope creep

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
