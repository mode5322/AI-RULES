# 10 — Security

## Purpose

Enforce secure defaults: secrets handling, authorization, input safety, and least privilege. This module is the **primary** security policy and AI review protocol — the **parent** of the **Security Laws** suite (قوانين الأمان). Companion modules **supplement, never replace**, this review:

| Suite role | Module | Responsibility |
|---|---|---|
| **Parent — policy / review** | `10-security.md` (this file) | Secrets, authz, input safety, least privilege; owns the suite |
| **Companion — defensive tools** | `18-security-tooling.md` | Optional stack-adaptive scanners (deps, secrets, Semgrep, ZAP baseline, platform checklists) |
| **Companion — discover → remediate** | `19-vuln-discovery-and-remediation.md` | Authorized discovery → triage → Remediation Closure Prompt/Plan → fix gate → re-verify |

**Reading order when security applies:** this file (`10`) first → `18` when tooling is enabled → `19` when findings exist or a discovery/remediation pass is in scope. Agents MUST treat `10` + `18` + `19` as **one Security Laws suite**, not as unrelated add-ons. MUST follow all applicable suite modules together.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE` (security is rarely N/A)

Current: _______________

## When this module applies / when to skip

- Applies to every change that can touch auth, data, files, network, payments, or user content.
- Never fully skip; only reduce depth for pure docs with no executable impact.
- Security refusals (illegal/harmful) are never deferred.
- Stack-adaptive hybrid: keep this policy/review always; add tooling from `18-security-tooling.md` only after question-protocol approval (or one-time deferral). Tool choice follows detected stacks — including mixed monorepos — see `18`.
- When scanner or review findings need closure, MUST follow `19-vuln-discovery-and-remediation.md` (authorized targets only; no exploits/PoCs; wait before fixes).

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
- MUST treat green scanner results as evidence, not as a substitute for this module’s review.
- When automated scans are appropriate, MUST follow `18-security-tooling.md` (defensive only; gated by questions).
- When findings (from `18` or this review) need triage/remediation, MUST follow `19-vuln-discovery-and-remediation.md` — Remediation Closure Plans, user choice before code changes (`15-error-handling.md`), no exploits or attack PoCs.

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
6. Optionally enable stack-adaptive defensive tooling (`18-security-tooling.md`) after question protocol.
7. Optionally enable discovery/remediation (`19-vuln-discovery-and-remediation.md`); route findings through Closure Plans before fixes.

## Existing-project workflow

1. Inventory auth, secrets, and admin surfaces.
2. Treat missing service-level checks as defects.
3. Remediate with compatibility-preserving fixes.
4. Rotate any exposed secrets discovered (instruct user; do not print secret values).
5. On audits, use `18-security-tooling.md` as a supplement to the manual/AI review — not a replacement.
6. Feed audit/tool findings into `19-vuln-discovery-and-remediation.md` for triage and Remediation Closure Plans (wait before code changes).

## Post-change checklist hooks

- [ ] No new hardcoded secrets
- [ ] Permission checks on sensitive actions
- [ ] Injection/XSS/path risks considered
- [ ] Logging safe
- [ ] Fail closed honored
- [ ] Tooling (if enabled) followed `18-security-tooling.md`
- [ ] Findings (if any) triaged/closed via `19-vuln-discovery-and-remediation.md` + `15-error-handling.md`

## PROJECT-SPECIFIC

- Auth system: _______________
- Roles / permissions map: _______________
- Secret mechanism: _______________
- Security contacts: _______________
- Known sensitive operations: _______________
- Compliance notes: _______________
- Security Laws suite — defensive tooling (`18`): ACTIVE | N/A | PROJECT-SPECIFIC | _______________
- Security Laws suite — vuln discovery/remediation (`19`): ACTIVE | N/A | PROJECT-SPECIFIC | _______________
