---
name: project-settings
description: Use whenever a skill needs a project preference (language, database, framework, connection) or the user asks about settings status. Reads the project profile Behavior and System design fields, and asks only about a field the current task needs.
---

# Project settings

The only settings list is **Behavior** and **System design** in `templates/project-profile.template.md` (or the consuming project's copy of that profile).

## Workflow
1. Read the profile. Do not create `.project/settings.md`.
2. If the repo already shows a fact, keep it. Do not ask.
3. If the current task does not use a field, leave it. Record `none` when that part is absent. Do not ask.
4. Ask one remaining relevant field using `references/question-protocol.md`.
5. Continue the task. Do not ask about colors, fonts, radius, icon libraries, or auth unless the current request is that choice and the repo does not show it.

## Rules
- Never overwrite a recorded profile value without the user asking to change it.
- If the user asks "what is unset?", list only relevant Behavior and System design blanks. Hide unrelated blanks unless they ask to see them.
