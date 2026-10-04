# Usage playbook

Short guide for installing `strict-ai-rules` into a user project.

## Install

Pick one:

- **Copy folders** into the project root: `laws/`, `templates/`, plus `AGENTS.md`, `CLAUDE.md`, and `.cursor/rules/strict-ai-rules.mdc` as needed.
- **Clone** this repo and merge the files into an existing app repo.
- **Subtree / submodule** if you want an upstream link (optional; most users just copy).

## After install

1. Open a chat and make a request, or ask the agent to configure the agent rules.
2. If the rules are not configured, the agent holds that first request and proposes rules setup (`laws/00-core.md`).
3. Ask it to configure the rules. It walks one section at a time, `00` through `19`, until every section is finished.
4. In an existing project, facts the code already shows (for example Firebase, Supabase, or SQL) are written automatically. The agent finishes that section or suggests the remaining choice.
5. In a new project, the agent asks. It does not invent project facts.
6. After setup is complete, the held request can proceed under the configured rules.

## New project flow

1. Rules-setup gate first (`00`): hold the first request, then configure each section before coding.
2. Requirements (`01`) → Discussion (`02`) → Architecture / UI / UX / DB / Security Laws suite (`10` + optional `18`/`19`) / branding-icons (`17`) happen inside that section walk.
3. Implement only after blocking questions are answered (or one-time deferral).
4. After each change: five-point review → final verification (`14`).

## Existing project flow

1. Rules-setup gate first (`00`). Code-backed facts (database and similar) are recorded during that walk.
2. Then start at `16-existing-projects.md` (+ `13-ai-review.md`).
3. Audit → rethink → issue/fix plan → confirm → fix.
4. Quick fix only when impact is isolated; otherwise root-cause with compatibility.
5. Security Laws suite: optional scanners `18-security-tooling.md` under parent `10`; actionable vulns via `19-vuln-discovery-and-remediation.md` (plan before fix; wait).

## Deferral

To skip questions once, or to skip rules setup for the current task only, say clearly you defer **for this time only** (see `templates/deferral.md`). Strict mode returns afterward. The agent holding the first request for rules setup is not this deferral.

## Keeping the origin clean

Do not push your project-specific filled laws back to the public `strict-ai-rules` origin. Customize only in your project copy.
