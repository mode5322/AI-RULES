# Usage playbook

Short guide for installing `strict-ai-rules` into a user project.

## Install

Pick one:

- **Copy folders** into the project root: `laws/`, `templates/`, plus `AGENTS.md`, `CLAUDE.md`, and `.cursor/rules/strict-ai-rules.mdc` as needed.
- **Clone** this repo and merge the files into an existing app repo.
- **Subtree / submodule** if you want an upstream link (optional; most users just copy).

## After install

1. Open a chat with your coding agent.
2. Tell it: “Read `AGENTS.md` and `laws/00-core.md`. This is [new | existing] project X. Fill PROJECT-SPECIFIC for this repo only.”
3. Answer questions using the 1–5 protocol (including Recommended).
4. Optionally fill `templates/project-profile.template.md` as your index.

## New project flow

1. Requirements (`01`) → Discussion (`02`) → Architecture / UI / UX / DB / security (`10`, optional tooling `18`, vuln pipeline `19`) / branding-icons (`17`) as needed.
2. Implement only after blocking questions are answered (or one-time deferral).
3. After each change: five-point review → final verification (`14`).

## Existing project flow

1. Start at `16-existing-projects.md` (+ `13-ai-review.md`).
2. Audit → rethink → issue/fix plan → confirm → fix.
3. Quick fix only when impact is isolated; otherwise root-cause with compatibility.
4. Optional defensive scanners: `18-security-tooling.md` (supplements `10`; stack-adaptive; question-gated).
5. Actionable vulns: `19-vuln-discovery-and-remediation.md` (plan before fix; wait).

## Deferral

To skip questions once: say clearly you defer **for this time only** (see `templates/deferral.md`). Strict mode returns afterward.

## Keeping the origin clean

Do not push your project-specific filled laws back to the public `strict-ai-rules` origin. Customize only in your project copy.
