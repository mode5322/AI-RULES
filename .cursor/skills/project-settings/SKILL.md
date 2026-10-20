---
name: project-settings
description: Use whenever a skill needs a project preference (colors, fonts, icon library, UI style, backend, database, language, direction, test commands) or the user asks about settings status. Reads and writes .project/settings.md, shows the count of unset settings, and asks only about settings relevant to the current task.
---

# Project settings

Single source of truth: `.project/settings.md` inside the user's project (never inside these skills).

## Workflow
1. If `.project/settings.md` is missing, create it from `template.md` in this folder. Do not ask anything yet.
2. Read it. Find settings the CURRENT task needs whose status is `unset`.
3. Auto-detect first (see project-discovery). Detected facts are saved as `set` with source `detected`, without asking.
4. Ask the remaining ones following `references/question-protocol.md`.
5. Counter = number of rows with status `unset` / total rows. Show it before each settings question.
6. After saving, continue the original task. Do not ask about the rest.

## Rules
- Statuses: `set`, `unset`, `agent-default`.
- Never overwrite a `set` value without asking.
- If the user asks "what is unset?", list the unset rows grouped by area.
- Project vocabulary goes in `GLOSSARY.md` (template: `glossary-template.md`). Use those terms in code and replies.
