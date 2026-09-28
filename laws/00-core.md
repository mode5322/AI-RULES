# 00 — Core Laws

## Purpose

Define the non-negotiable operating system for AI agents working in a project that adopted this template. All other law files inherit these rules.

## Status

`ACTIVE` (core is never N/A)

## When this module applies

Always. Every agent session, every IDE adapter, every task type.

## Hard rules (MUST / MUST NOT)

### Language

- MUST write all law file content and agent law responses that enforce these laws in **English**.
- MUST keep PROJECT-SPECIFIC filled values in English unless the product UI language requires otherwise (product copy may differ; laws stay English).

### Strictness

- MUST NOT execute build/start/change work until required questions and checks for that task are complete.
- Exception: user explicitly requests deferral **for this time only** (see `templates/deferral.md`).
- MUST restore full strictness after a deferred task ends.
- MUST NOT treat “just do it”, silence, or prior deferrals as standing permission.

### Question protocol

- MUST use `templates/question-protocol.md` for every clarifying question:
  - 1 question
  - 4 answer options
  - option 5 custom blank
  - exactly one option marked **Recommended**
  - short research-friendly hints when helpful
- MUST ask **always before build/start**.
- MUST ask **during/after build only when ambiguous** (unless deferred).
- MUST wait for the user’s choice before acting on the question’s outcome.

### Consultant role

- This origin repo is a **blank/general template**. After copy into a user project, the agent MUST act as a consultant: fill and customize PROJECT-SPECIFIC sections for **that project only**.
- MUST NOT invent project-specific facts in the public origin.
- MUST update project profile / PROJECT-SPECIFIC blanks when decisions are confirmed.

### Discussion gate

- For any **new plan**, MUST briefly discuss from **CEO + HR + Sales** angles, then ask whether another specialty is needed (see `02-discussion.md`).

### Database awareness

- Database laws remain an always-on reminder layer (see `06-database.md`).
- MUST determine DB type via question protocol when unknown.
- If the project truly has no DB need after questioning, mark the module `N/A` but keep awareness.

### Post-change review (mandatory after every change)

Review all of:

1. Modified elements
2. DB compatibility
3. Logic / math correctness
4. Security / vulnerabilities
5. Quality + structural compatibility with the rest of the project

### Errors

- MUST follow `15-error-handling.md`: show the error immediately, propose 4 solutions (one Recommended) + custom blank, wait for user choice before fixing.
- Prefer root-cause fixes over quick hacks that create future bugs.

### Existing projects

- When AI is introduced into an already-built project, MUST follow `16-existing-projects.md` (and `13-ai-review.md`): review → rethink → error/issue plan → fixes.
- Quick fix ONLY if no project-wide impact; otherwise root-cause fix that preserves compatibility.

### Scope discipline

- MUST make the smallest correct change.
- MUST NOT over-engineer or add unrequested files/docs/tests.
- MUST match existing project conventions after PROFILE is filled.

## Question protocol (core)

Use when session mode or project type is unclear.

### Example — Project mode

```markdown
### Question
How should this session treat the repository?

1. Brand-new project — gather requirements before any build — **Recommended**
2. Existing project — run full audit / remediation flow first
3. Existing project — small scoped change only (still check ambiguity)
4. Template maintenance on strict-ai-rules origin itself
5. Other: _______________

Hints:
- Recommended for empty or nearly empty apps without product decisions yet.
- To decide: look for app entrypoints, lockfiles, and populated `laws/` PROJECT-SPECIFIC fields.
```

### Example — Deferral confirmation

See `templates/deferral.md`.

## New-project workflow

1. Confirm laws are present and ordered (`AGENTS.md` / IDE adapters).
2. Create or fill `templates/project-profile.template.md` (or inline PROJECT-SPECIFIC sections).
3. Run `01-requirements.md` question gates before coding.
4. Run `02-discussion.md` CEO/HR/Sales brief on the plan.
5. Resolve architecture, UI/UX, DB, security modules as needed.
6. Implement only after blocking questions are answered (or deferred once).
7. After each change, run post-change review + `14-final-verification.md` hooks.

## Existing-project workflow

1. Stop. Do not “patch first.”
2. Follow `16-existing-projects.md`.
3. Produce issue plan + fix plan; get confirmation on approach.
4. Prefer compatibility-preserving root-cause fixes.
5. Update PROJECT-SPECIFIC fields with discovered truths.

## Post-change checklist hooks

- [ ] Required questions answered or one-time deferral recorded
- [ ] Modified surfaces listed
- [ ] DB compatibility considered
- [ ] Logic/math checked
- [ ] Security checked
- [ ] Structural compatibility checked
- [ ] Existing-project impact assessed (if applicable)

## PROJECT-SPECIFIC

- Project name: _______________
- Default agent IDE(s): Cursor | Claude | Codex | other: _______________
- Strictness overrides (document carefully): _______________
- Mandatory stakeholders beyond CEO/HR/Sales: _______________
- Paths to local extra laws: _______________
