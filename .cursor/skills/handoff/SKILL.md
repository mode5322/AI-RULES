---
name: handoff
description: Use when the conversation is getting long, the agent starts forgetting rules, or the user asks to continue in a new chat. Writes .project/handoff.md so a fresh agent session can continue the work.
---

# Handoff

Write `.project/handoff.md` (overwrite) with:
1. Goal of the current work.
2. Current state: done, in progress, broken.
3. Decisions made and why (short).
4. Files touched and their role.
5. Open issues and the exact next step.
6. Pointer: settings are in `.project/settings.md`, vocabulary in `GLOSSARY.md`.

Keep it under about 60 lines. Tell the user to start a new chat and say: "Read .project/handoff.md and continue."
