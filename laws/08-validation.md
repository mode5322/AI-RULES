# 08 — Validation

## Purpose

Ensure all inputs are validated and rejected safely before persistence, API calls, or side effects.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`


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

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. List entities and fields; mark required/optional.
2. Choose canonical validation layer.
3. Define shared error message style.
4. Implement validators reused by UI and services.
5. Reject invalid input at the trust boundary. Do not add a settings blank.

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

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
