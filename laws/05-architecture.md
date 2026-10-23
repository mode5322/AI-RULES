# 05 — Architecture

## Purpose

Keep structure intentional: clear layers, naming, and boundaries so features stay maintainable.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`


## When this module applies / when to skip

- Applies: new modules, refactors, cross-cutting changes, bootstrap of folder layout.
- Lightweight apply: small fixes must still respect existing boundaries.
- `N/A` only for docs-only / non-code chores.

## Hard rules (MUST / MUST NOT)

- MUST read surrounding structure before adding files.
- MUST follow the project’s chosen layout once PROFILE is filled.
- MUST keep layer boundaries (e.g. screens compose; services orchestrate; database access isolated; utils stay pure) when that model is adopted.
- MUST NOT place business rules only in UI controls.
- MUST NOT introduce a second parallel architecture style without an explicit decision.
- MUST prefer extending existing modules over creating near-duplicates.
- MUST keep the change small; no speculative frameworks.
- Before build/start, MUST clarify architecture when unknown.
- Branding / app icon asset trees and source-of-truth vs generated platform exports MUST follow `17-branding-and-icons.md` — do not scatter identity assets or invent a second branding layout without a decision.

### Suggested default layout (adapt to stack)

```
screens/      # page-level UI
components/   # reusable UI (group by screen/service when needed)
services/     # business orchestration + exports barrel
utils/        # pure helpers
database/     # schema + data access API
types/        # shared types
hooks/        # reusable hooks if applicable
```

Adapt names to the stack (e.g. `app/`, `src/`, `lib/`) but keep role clarity.

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Choose architecture style via questions.
2. Create skeleton folders matching the decision.
3. Match the naming already in the repo. Do not open a naming questionnaire.
4. Add services barrel / public entrypoints if applicable.
5. Implement features inside the agreed boundaries.

## Existing-project workflow

1. Map the real architecture (not the aspirational one).
2. New code MUST match the dominant real pattern unless a migration plan exists.
3. If patterns conflict, propose a compatibility-preserving consolidation plan (see `16-existing-projects.md`).
4. Do not “fix” structure with a wide rewrite unless approved.

## Post-change checklist hooks

- [ ] Files landed in the correct layer/folder
- [ ] No boundary violations (UI bypassing services, etc.)
- [ ] Naming matches conventions
- [ ] No duplicate module introduced

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
