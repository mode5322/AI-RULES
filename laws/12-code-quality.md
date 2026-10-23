# 12 — Code Quality

## Purpose

Keep code readable, consistent, and maintainable without gold-plating.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`


## When this module applies / when to skip

- Applies to all code changes.
- Depth scales with risk; still no sloppy shared-module edits.

## Hard rules (MUST / MUST NOT)

- Before naming or adopting a library, tool, algorithm, or external feature, follow **Current sources** in `00-core.md`.
- MUST match existing naming, formatting, and abstractions.
- MUST reuse existing helpers/components instead of reimplementing.
- MUST keep functions focused; avoid huge catch-all modules for new code.
- MUST NOT over-engineer: no extra layers “for the future.”
- MUST NOT add unsolicited docs, comments, or refactors.
- Comment only non-obvious business logic **or** deliberate-simplification markers (below).
- MUST delete dead code introduced by the change when safe.
- MUST keep types accurate when the project is typed.
- After changes: include quality + structural compatibility in mandatory review.

### Implementation ladder (MUST stop at first rung that holds)

1. **YAGNI** — Does this need to exist? Speculative need → skip; say so in one line.
2. **Stdlib** — Prefer language/standard library.
3. **Native platform** — Prefer built-in platform/HTML/CSS/DB features over custom code or new libs.
4. **Installed dependency** — Reuse what is already in the project. MUST NOT add a new library unless the user asks for something the installed libraries do not provide. Then add the one library that provides that capability (for example icons). MUST NOT add a second library for a capability an installed library already covers.
5. **Fewest lines** — Prefer one-liners / shortest correct form when readable.
6. **Minimum that works** — Only then write the smallest correct implementation.

### Anti-abstraction rules

- MUST NOT add: single-implementation interfaces, factories for one product, config for values that never change, wrappers that only delegate, scaffolding “for later.”
- Prefer **deletion over addition**; boring over clever; **fewest files**; **shortest working diff**.
- Prefer the stdlib option that is **correct on edge cases** when two options are similar size.

### Never simplify away

MUST NOT cut: input validation at trust boundaries, error handling that prevents data loss, security measures, accessibility basics, or anything explicitly requested. User insists on the full version → build it without re-arguing.

### Intensity levels

| Level | Behavior |
|---|---|
| **lite** | Build what was asked; name a lazier alternative in one line; user picks. |
| **full** | Ladder enforced. Stdlib/native first. Shortest correct diff. **Default.** |
| **ultra** | YAGNI extremist. Deletion before addition. Ship the minimum and challenge extra requirements in the same breath (still after question gates). |

- Default **full** unless `00-core` / PROFILE sets otherwise.
- Switch only when the user asks (`lite` / `full` / `ultra`) or PROFILE is updated.

### Deliberate-simplification markers (debt comments)

When leaving a conscious shortcut with a known ceiling, mark it in code:

```text
// simplify: <ceiling>, <upgrade when / path>
```

(Use the project’s comment syntax. Alias `ponytail:` is acceptable if already present in a codebase.)

- MUST name both the **ceiling** and the **upgrade trigger** when possible.
- Markers feed the debt ledger pass in `13-ai-review.md` / `16-existing-projects.md`.

### Minimal runnable check for non-trivial logic

Non-trivial logic (branch, loop, parser, money/security path) SHOULD leave the smallest runnable check that fails if the logic breaks (one assert/self-check or one small test), unless `09-testing.md` / PROFILE forbids it. Trivial one-liners need no extra test.

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Establish formatter/linter early if the stack expects it.
2. Set intensity in PROFILE (default full).
3. Write boring, clear, ladder-first code.
4. Create shared helpers only when reuse is real.
5. Match the conventions already in the repo. Do not add a settings blank.

## Existing-project workflow

1. Mirror local style even if you prefer another.
2. Don’t reformat unrelated files.
3. Apply the ladder to **new** code; don’t mass-rewrite for style.
4. Over-engineering and bloat findings go into remediation (`13` / `16`), not drive-by rewrites.

## Post-change checklist hooks

- [ ] Style matches neighbors
- [ ] Ladder applied; no speculative abstractions
- [ ] No unjustified new dependencies
- [ ] Deliberate shortcuts marked with ceiling + upgrade trigger
- [ ] Types/lint clean for touched scope (as project requires)
- [ ] Structural compatibility OK

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
