# 15 — Error Handling

## Purpose

Standardize how agents respond to errors and failures: surface immediately, propose options, wait for the user, then fix with root-cause preference.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`

Current: _______________

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

## Question protocol extras

### Example — After user picks a fix

If the chosen fix is still ambiguous:

```markdown
### Question
Confirm fix scope for the selected approach?

1. Fix only the failing path — **Recommended**
2. Fix shared root + update callers
3. Fix + add regression test/check
4. Revert to last known good, then redo carefully
5. Other: _______________
```

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
4. Record recurring errors in PROJECT-SPECIFIC.

## Post-change checklist hooks

- [ ] User choice recorded
- [ ] Fix matches choice
- [ ] Root-cause preferred unless isolated quick fix approved
- [ ] Five-point review after fix

## PROJECT-SPECIFIC

- Logging approach: _______________
- User-facing error style: _______________
- On-call / owner: _______________
- Recurring error catalog path: _______________
- Changes that always require rollback plan: _______________
