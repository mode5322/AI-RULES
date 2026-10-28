# Question Protocol (Canonical)

Show this format only when both are true:

1. A decision is necessary (the work cannot proceed without it, and the repo does not already prove the value).
2. The user asks to see options. The fixed phrases are «عرض خيارات» and "Show options".

Until then, state the necessary point in one short line. Do not show numbered options. Do not ask deferral or ignore settings (`templates/deferral.md`).

## Rules

1. Ask **exactly one** question at a time.
2. Offer **at least four** concrete answer options. More than four is allowed when the choice set needs it (including totals above five).
3. End with a final **Other: _______________** custom blank (always the last numbered option).
4. Mark **exactly one** concrete option (not Other) as **Recommended**.
5. When helpful, add short **research-friendly suggestion hints** under options (search terms, docs to check, or trade-offs). If a hint states how a technology, website, reference, feature, algorithm, tool, or library works, review its current authoritative source first (`laws/00-core.md`, Current sources).
6. Wait for the user's choice (or custom answer) before continuing. If the question is asked in Arabic, format Latin spans using Behavior → `Arabic mixed-script display` from `laws/00-core.md` (Language). Default until set: `unicode-rtl-lri`.
7. Do not batch multiple independent questions into one message unless the user explicitly deferred clarification for this time only (see `templates/deferral.md`).
8. Prefer the shortest clear option list. Add extra concrete options only when they change the decision; do not pad.

## Template

```markdown
### Question
<one clear question that this task cannot proceed without>

1. <option A>
2. <option B> — **Recommended**
3. <option C>
4. <option D>
5. Other: _______________
```

Do not copy a sample question into a project that does not need that decision.

## Anti-patterns (MUST NOT)

- Asking a question that does not connect to the current project, unless the user asked to see that question
- Showing this option list before the user says «عرض خيارات» or "Show options"
- Asking the user to configure deferral or ignore settings
- Fewer than four concrete options (unless the domain truly has fewer mutually exclusive choices — then still end with Other)
- More than one primary question per turn (unless deferred)
- Hiding the Recommended marker
- Proceeding after asking without waiting for an answer
- Using the protocol for trivia that does not change the plan
- Padding with near-duplicate options
