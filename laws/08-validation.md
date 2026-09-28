# 08 — Validation

## Purpose

Ensure all inputs are validated and rejected safely before persistence, API calls, or side effects.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`

Current: _______________

## When this module applies / when to skip

- Applies: forms, APIs, file uploads, imports, agent-provided data written to the system.
- Never skip for security-critical fields (auth, money, permissions, PII).
- Soft skip only for static content edits with no input pipeline.

## Hard rules (MUST / MUST NOT)

- MUST validate and sanitize user input before save, API calls, or file writes.
- MUST NOT trust client-only checks for security-critical rules.
- MUST return clear user-facing messages (use project language for product copy).
- MUST fail closed on unknown/invalid permission or unchecked state.
- MUST define required vs optional fields explicitly.
- MUST validate types, ranges, formats, and referential existence where needed.
- MUST keep server/service validation even if UI validates.
- During ambiguity (which fields/rules?), ask before building.

## Question protocol

### Example — Validation placement

```markdown
### Question
Where should canonical validation run?

1. Service/domain layer (UI mirrors for UX) — **Recommended**
2. UI only
3. Database constraints only
4. API gateway schemas only
5. Other: _______________
```

### Example — Invalid input UX

```markdown
### Question
How should validation failures be shown?

1. Per-field messages + summary if many — **Recommended**
2. Single toast with first error only
3. Blocking modal listing all errors
4. Inline only on submit blur
5. Other: _______________
```

### Example — Strictness on imports

```markdown
### Question
How should bulk import rows fail?

1. Reject row with errors; import valid rows; report summary — **Recommended**
2. Reject entire file on any error
3. Import all; quarantine invalid rows for review
4. Auto-coerce when possible; flag coercions
5. Other: _______________
```

## New-project workflow

1. List entities and fields; mark required/optional.
2. Choose canonical validation layer.
3. Define shared error message style.
4. Implement validators reused by UI and services.
5. Add edge-case examples to PROJECT-SPECIFIC.

## Existing-project workflow

1. Discover existing validation libraries/patterns.
2. Extend them; don’t invent a parallel validator.
3. Close holes where UI-only checks protect money/permissions.
4. Root-cause invalid data already stored (migration/cleanup plan if needed).

## Post-change checklist hooks

- [ ] Service-level validation present for critical paths
- [ ] Messages clear
- [ ] No trust of client-only enforcement
- [ ] Ranges/formats covered
- [ ] Post-change validation of critical paths uses command/live proof when required (`09-testing.md`) — not theory-only

## PROJECT-SPECIFIC

- Validation library: _______________
- Canonical layer: _______________
- Error message language: _______________
- Required field policy: _______________
- Import failure policy: _______________
- Sanitization notes: _______________
