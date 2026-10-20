# Question protocol (shared by all skills)

Ask in the user's language (default: Arabic). Instructions here stay in English.

1. Ask only what the CURRENT task needs. Never ask about unrelated areas.
2. Group at most 3 related questions per turn. Unrelated questions wait.
3. Each question: 2-4 short options + one marked "(recommended)" + an option "Custom".
4. If the user says "you decide" / "قرر أنت": save the recommended option with status `agent-default`.
5. If the user says "this time only": use the value for the task, do NOT save it.
6. Start every settings question with the counter: "Unset settings: N of M".
7. Save every answer immediately to `.project/settings.md` (see project-settings skill).
