# 15 — Error Handling

## Purpose

Standardize how agents respond to errors and failures: surface immediately, propose options, wait for the user, then fix with root-cause preference.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`


## When this module applies / when to skip

- Applies to build failures, runtime errors, test failures, migration errors, and logical defects discovered mid-work.
- Applies when the agent is unsure which fix strategy to use.
- Applies to **terminal-observed failures** during command or live testing (`09-testing.md`): use captured stdout/stderr/exit codes/logs as the error context for this protocol.
- Applies to **security findings** from reviews or defensive scanners: present the finding + solutions and wait — after (or with) the remediation plan in `19-vuln-discovery-and-remediation.md`. Policy remains `10-security.md`; scanners remain `18-security-tooling.md`.
- Never skip waiting for user choice unless one-time deferral explicitly covers fix selection.

## Hard rules (MUST / MUST NOT)

- MUST show the error immediately (clear message; include relevant context, not huge unrelated dumps).
- When the failure was seen during command/live testing, MUST ground the error statement in **terminal-observed** evidence (see `09-testing.md`), then offer solution steps via this protocol.
- MUST propose **exactly four** solutions + **option 5 custom blank**.
- MUST mark **exactly one** solution **Recommended**.
- MUST **wait for the user’s choice before fixing**.
- MUST prefer root-cause solutions over quick hacks that create future bugs.
- MUST NOT silently retry destructive operations.
- MUST NOT hide errors behind “it works on my machine” assumptions.
- Quick fix may be Recommended only when impact is isolated and residual risk is low; otherwise Recommend root-cause.
- For security findings: MUST NOT skip `19-vuln-discovery-and-remediation.md` plan + law gates before offering solutions.
- After the chosen fix: run mandatory five-point review.

## User-facing diagnosis brief (when the user does not know the cause)

When the user asks what went wrong and clearly does **not** already know the cause, MUST lead with this short brief (skill `problem-brief`) before the solutions block:

```text
مكان المشكلة = <path or URL where the failure appears>
سبب المشكلة = ملف (<filename>), <short cause>
حل المشكلة = <primary fix: move/copy/create what → where>
حل المشكلة بطريقة أخرى = يجب تعديل <what> في الملف "<file path>" في السطر رقم "<N>"
يجب أن يكون "<exact expected line, value, or shape>"
```

Then continue with the solutions template below and wait.

## Error response template

```markdown
### Error
<concise error statement>
Where: <file/command/flow>
Impact: <what breaks>

### Solutions
1. <solution A>
2. <solution B> — **Recommended**
3. <solution C>
4. <solution D>
5. Other: _______________

Hints:
- Recommended because: <root-cause / safety reason>
- Trade-off: <speed vs durability>
```

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. On first failure, stop implementation thrash.
2. Present error + 4 solutions + custom.
3. Wait.
4. Apply chosen fix.
5. Re-verify; continue only if clean or newly re-triaged.

## Existing-project workflow

1. Classify: local bug vs systemic design issue.
2. If systemic, Recommended solution should be root-cause with compatibility notes.
3. Align with `16-existing-projects.md` — don’t band-aid architecture breaks.
4. State a recurring error in the reply. Do not add a settings blank.

## Post-change checklist hooks

- [ ] User choice recorded
- [ ] Fix matches choice
- [ ] Root-cause preferred unless isolated quick fix approved
- [ ] Five-point review after fix

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
