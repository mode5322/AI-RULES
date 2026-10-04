# 12 — Code Quality

## Purpose

Keep code readable, consistent, and maintainable without gold-plating.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`

Current: _______________

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
4. **Installed dependency** — Reuse what is already in the project; MUST NOT add a new dependency for what a few lines can do.
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

### Example — Quality bar for this task

```markdown
### Question
What quality bar should we apply?

1. Match surrounding code; fix only what we touch — **Recommended**
2. Opportunistic cleanup in the same files if low risk
3. Broader refactor of the module
4. Strict lint/type clean for the whole package
5. Other: _______________
```

### Example — Minimal-implementation intensity

```markdown
### Question
Which minimal-implementation intensity should apply for this work?

1. full — ladder enforced; shortest correct diff — **Recommended**
2. lite — build as asked; name the lazier alternative
3. ultra — maximum YAGNI; challenge extras in the same response
4. Keep PROFILE default (no change this session)
5. Other: _______________
```

### Example — Duplication

```markdown
### Question
We found duplicated logic. What should we do?

1. Extract a shared helper now if ≥2 call sites and stable behavior — **Recommended**
2. Leave duplication for this pass; note follow-up
3. Rewrite all call sites to a new abstraction
4. Keep copies intentional (document why)
5. Other: _______________
```

## New-project workflow

1. Establish formatter/linter early if the stack expects it.
2. Set intensity in PROFILE (default full).
3. Write boring, clear, ladder-first code.
4. Create shared helpers only when reuse is real.
5. Record conventions and forbidden patterns in PROJECT-SPECIFIC.

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

- Formatter / linter: _______________
- Naming conventions: _______________
- Max complexity preferences: _______________
- Minimal-implementation intensity default: lite | full | ultra: _______________
- Comment policy: _______________
- Simplification marker prefix (`simplify:` / `ponytail:` / other): _______________
- Forbidden patterns: _______________
