# 10 — Security

## Purpose

Enforce secure defaults: secrets handling, authorization, input safety, and least privilege.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE` (security is rarely N/A)

Current: _______________

## When this module applies / when to skip

- Applies to every change that can touch auth, data, files, network, payments, or user content.
- Never fully skip; only reduce depth for pure docs with no executable impact.
- Security refusals (illegal/harmful) are never deferred.

## Hard rules (MUST / MUST NOT)

### Secrets

- MUST NOT hardcode API keys, tokens, passwords, or credentials in source.
- MUST use environment variables, OS secret storage, or the project’s secret mechanism.
- MUST NOT commit `.env` or credential files.
- MUST warn if the user asks to commit secrets.

### Authorization

- MUST check permissions for sensitive actions (delete, refund, price override, admin, export).
- MUST enforce authorization in the service layer, not only by hiding UI.
- MUST fail closed when permission is unknown or unchecked.

### Input & output

- MUST validate/sanitize untrusted input.
- MUST avoid injection (SQL, command, template, HTML) via parameterized APIs and safe rendering.
- MUST NOT log secrets or full sensitive payloads.

### General

- MUST prefer least privilege for tokens, DB users, and file access.
- MUST review for vulnerabilities after every change (mandatory review item).
- MUST NOT weaken security to “just make it work” without explicit one-time deferral **and** a follow-up fix plan.

## Question protocol

### Example — Auth method

```markdown
### Question
Which authentication approach should this project use?

1. Existing project auth — keep it — **Recommended**
2. Session cookies + server sessions
3. Token/JWT based API auth
4. External identity provider (OAuth/OIDC)
5. Other: _______________
```

### Example — Role model

```markdown
### Question
How should authorization be modeled?

1. Role-based access control (RBAC) with service checks — **Recommended**
2. Simple admin vs non-admin flag
3. Permission flags per action
4. No auth required for this product surface
5. Other: _______________
```

### Example — Secret storage

```markdown
### Question
Where should secrets live?

1. `.env` locally + host secret store in deployment — **Recommended**
2. Cloud secret manager only
3. OS keychain / secure storage (desktop apps)
4. Hardcoded in repo (not allowed)
5. Other: _______________
```

## New-project workflow

1. Choose auth and role model early.
2. Define secret handling and `.gitignore` entries.
3. Build service-level permission helpers before admin features.
4. Threat-note sensitive flows in PROJECT-SPECIFIC.
5. Run security review on first vertical slice.

## Existing-project workflow

1. Inventory auth, secrets, and admin surfaces.
2. Treat missing service-level checks as defects.
3. Remediate with compatibility-preserving fixes.
4. Rotate any exposed secrets discovered (instruct user; do not print secret values).

## Post-change checklist hooks

- [ ] No new hardcoded secrets
- [ ] Permission checks on sensitive actions
- [ ] Injection/XSS/path risks considered
- [ ] Logging safe
- [ ] Fail closed honored

## PROJECT-SPECIFIC

- Auth system: _______________
- Roles / permissions map: _______________
- Secret mechanism: _______________
- Security contacts: _______________
- Known sensitive operations: _______________
- Compliance notes: _______________
