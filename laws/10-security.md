# 10 — Security

## Purpose

Enforce secure defaults: secrets handling, authorization, input safety, and least privilege. This module is the **primary** security policy and AI review protocol — the **parent** of the **Security Laws** suite (قوانين الأمان). Companion modules **supplement, never replace**, this review:

| Suite role | Module | Responsibility |
|---|---|---|
| **Parent — policy / review** | `10-security.md` (this file) | Secrets, authz, input safety, least privilege; owns the suite |
| **Companion — tools + audit skill** | `18-security-tooling.md` | Optional scanners + vendored `.cursor/skills/security-audit/` (Cloudflare MIT skill) |
| **Companion — discover → remediate** | `19-vuln-discovery-and-remediation.md` | Authorized discovery → triage → Remediation Closure Prompt/Plan → fix gate → re-verify |

**Reading order when security applies:** this file (`10`) first → `18` when tooling is enabled → `19` when findings exist or a discovery/remediation pass is in scope. Agents MUST treat `10` + `18` + `19` as **one Security Laws suite**, not as unrelated add-ons. MUST follow all applicable suite modules together.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE` (security is rarely N/A)


## When this module applies / when to skip

- Applies to every change that can touch auth, data, files, network, payments, or user content.
- Never fully skip; only reduce depth for pure docs with no executable impact.
- Security refusals (illegal/harmful) are never deferred.
- Stack-adaptive hybrid: keep this policy/review always; add tooling from `18-security-tooling.md` only after question-protocol approval (or one-time deferral). Tool choice follows detected stacks — including mixed monorepos — see `18`.
- When scanner or review findings need closure, MUST follow `19-vuln-discovery-and-remediation.md` (authorized targets only; wait before fixes).

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
- When automated scans or a multi-phase audit are appropriate, MUST follow `18-security-tooling.md` (track A scanners and/or track B `security-audit` skill; gated by user request / questions).
- When findings (from `18`, the `security-audit` skill, or this review) need triage/remediation, MUST follow `19-vuln-discovery-and-remediation.md` — Remediation Closure Plans, user choice before code changes (`15-error-handling.md`).

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Choose auth and role model early.
2. Define secret handling and `.gitignore` entries.
3. Build service-level permission helpers before admin features.
4. Keep secrets and authorization checks in the change. Do not add a settings blank.
5. Run security review on first vertical slice.
6. Optionally enable stack-adaptive tooling (`18-security-tooling.md`, including the `security-audit` skill) after question protocol / audit request.
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

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
