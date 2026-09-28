# 16 — Existing Projects

## Purpose

Dedicated protocol for repositories that already exist when AI (and these laws) are introduced later. Prevents reckless patching and forces review → rethink → plan → fix.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → use `ACTIVE` when the consuming repo is not greenfield

Current: _______________

## When this module applies / when to skip

- Applies when the project has substantial existing code, data, or users.
- Applies when the user says “we added AI to an old project,” “audit this,” or “fix what’s broken.”
- Skip only for true greenfield (use new-project flows in other laws).
- Referenced from `00-core.md` and `13-ai-review.md`.

## Hard rules (MUST / MUST NOT)

- MUST review the whole project (proportionate depth) before large changes.
- MUST rethink: separate symptoms from root causes.
- MUST propose a plan of **current issues + fixes** before mass edits.
- MUST run `02-discussion.md` (CEO/HR/Sales) when the remediation is a new plan.
- Quick fix ONLY if there is **no project-wide impact**.
- Otherwise MUST apply a **root-cause fix** that preserves compatibility with the rest of the project.
- MUST NOT rewrite the architecture casually.
- MUST NOT ignore existing DB engine, auth, or UI system.
- MUST update PROJECT-SPECIFIC with discovered realities (not aspirational fiction).
- MUST use question protocol before choosing remediation strategy.
- MUST follow `15-error-handling.md` for runtime failures during remediation.

## Question protocol

### Example — Engagement type

```markdown
### Question
How should we engage this existing project?

1. Full audit → rethink → issue/fix plan → implement — **Recommended**
2. Scoped audit of one area, then fix that area
3. Single bug hunt only (still check blast radius)
4. Documentation/profile fill only; no code yet
5. Other: _______________
```

### Example — Fix policy

```markdown
### Question
When an issue has wide impact, what fix policy applies?

1. Root-cause, compatibility-preserving fix — **Recommended**
2. Isolated quick fix + tracked follow-up
3. Feature flag + gradual migration
4. Freeze feature work until redesign approved
5. Other: _______________
```

### Example — Compatibility constraint

```markdown
### Question
Which compatibility constraint is strictest right now?

1. Keep DB schema backward compatible — **Recommended**
2. Keep public API compatible
3. Keep UI flows/muscle memory stable
4. Keep file/folder layout stable
5. Other: _______________
```

## Existing-project workflow (canonical)

1. **Stop and frame** — confirm this is an existing-project engagement.
2. **Inventory** — languages, frameworks, entrypoints, environments, DB, auth, deploy.
3. **Review** — critical defects first (data loss, security, money, crashes), then major consistency issues.
4. **Rethink** — map root causes; note constraints.
5. **Plan** — ordered issues with severity and proposed fixes; brief CEO/HR/Sales if plan-level.
6. **Confirm** — question protocol on sequencing and fix policy.
7. **Fix** — implement approved items; quick fix only when isolated.
8. **Verify** — five-point review + `14-final-verification.md`.
9. **Record** — fill profile / PROJECT-SPECIFIC; keep origin template blank.

## New-project note

If the repo is actually greenfield, mark this module `N/A` and use modules `01`–`15` new-project flows.

## Post-change checklist hooks

- [ ] Plan existed before mass edits
- [ ] Compatibility preserved or change approved
- [ ] Quick vs root-cause policy honored
- [ ] Audit notes updated

## PROJECT-SPECIFIC

- Repo age / maturity: _______________
- Known debt themes: _______________
- Hard compatibility constraints: _______________
- Audit report path: _______________
- Remediation board / checklist: _______________
- Areas that must not be drive-by edited: _______________
