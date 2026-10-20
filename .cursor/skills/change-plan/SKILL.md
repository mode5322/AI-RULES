---
name: change-plan
description: Use before a change that touches more than 3 files, an existing project's structure, the database schema, dependencies, or deletes files. Presents a short plan and waits for approval before editing.
---

# Change plan

Skip for small, single-file changes.

1. Present, in the user's language and briefly:
   - Goal in one sentence.
   - Files to create / modify / delete.
   - Dependency or schema changes.
   - Main risk and how to undo it.
2. Ask for approval (approve / edit plan / cancel).
3. Only after approval, apply the `git-checkpoint` skill, then implement.
4. If scope grows during work, stop and update the plan.
