# 11 — Change Management

## Purpose

Control how changes are planned, applied, reviewed, and rolled back so the project stays coherent.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`

Current: _______________

## When this module applies / when to skip

- Applies to every code or schema change.
- Lightweight for tiny copy fixes; full for schema, auth, payments, refactors.
- Works with `14-final-verification.md` and `16-existing-projects.md`.

## Hard rules (MUST / MUST NOT)

- MUST state the intent of a change before editing when the task is non-trivial.
- MUST make the smallest correct change.
- MUST apply the `12-code-quality.md` implementation ladder to the chosen approach (after gates).
- MUST NOT mix unrelated refactors into a bugfix.
- MUST assess blast radius: screens, services, DB, callers.
- MUST run the mandatory post-change review:
  1. Modified elements
  2. DB compatibility
  3. Logic/math
  4. Security/vulns
  5. Quality + structural compatibility
- MUST prefer root-cause fixes over temporary patches.
- MUST NOT use one-off migration hacks or single-run scripts as the durable fix when a proper path exists.
- Quick fix ONLY when there is **no project-wide impact**; otherwise plan a compatible root-cause fix.
- MUST NOT commit unless the user explicitly asks (agent rule).
- Schema/data changes require migration discipline from `06-database.md`.

## Question protocol

### Example — Change strategy

```markdown
### Question
How should we apply this change?

1. Minimal localized fix with post-change review — **Recommended**
2. Root-cause fix touching shared modules (compatibility-preserving)
3. Phased plan: patch now + scheduled root-cause follow-up
4. Design-only proposal first; no code yet
5. Other: _______________

Hints:
- Prefer 2 when the same bug class will recur.
- Prefer 1 only when impact is truly isolated.
```

### Example — Risk tolerance

```markdown
### Question
What risk posture should we take?

1. Conservative — preserve behavior; additive changes — **Recommended**
2. Aggressive cleanup / rewrite of the touched area
3. Feature-flagged rollout
4. Branch experiment then merge
5. Other: _______________
```

## New-project workflow

1. Confirm requirements and discussion gates.
2. Choose change strategy if multiple approaches exist.
3. Implement smallest slice.
4. Run post-change review after each logical unit.
5. Verify with `14-final-verification.md`.

## Existing-project workflow

1. Map dependents before editing shared code.
2. Prefer compatible changes over breaking renames.
3. If a quick fix is requested but impact is wide, refuse the hack and propose root-cause options via error/solution protocol.
4. Document follow-ups in PROJECT-SPECIFIC when phased.

## Post-change checklist hooks

- [ ] Intent clear; scope minimal
- [ ] Blast radius assessed
- [ ] Five-point mandatory review done
- [ ] Rollback idea known for risky changes

## PROJECT-SPECIFIC

- Branching model: _______________
- Review requirements: _______________
- Migration windows: _______________
- Feature flag system: _______________
- Rollback notes: _______________
