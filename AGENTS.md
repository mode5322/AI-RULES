# AGENTS.md

Instructions for coding agents (Codex, Cursor Agent, and general LLM agents) working in a repository that includes this template.

## What this is

`strict-ai-rules` is a **strict law pack** for AI agents. After this folder is copied into a **user project**, agents must treat `laws/` as binding operating rules and customize `PROJECT-SPECIFIC` sections for **that project only**.

The public GitHub origin stays a blank/general template.

## Mandatory read order

Before non-trivial work, read:

1. `laws/00-core.md`
2. `templates/question-protocol.md`
3. `templates/deferral.md`
4. Then domain laws as relevant (`01`–`19`)
5. For existing codebases: `laws/16-existing-projects.md` and `laws/13-ai-review.md`

## Operating summary

- English-only law content. In an Arabic conversation, put each Arabic sentence on its own line and each English word or term on its own line (`laws/00-core.md`, Language). Do not embed an English term inside an Arabic line.
- When laws conflict, follow Law precedence in `laws/00-core.md`. A new chat resumes at the first unconfigured setting and does not re-ask configured ones. Merging a newer pack keeps configured values (`laws/11-change-management.md`). Product right-to-left layout is `laws/03-ui.md`, not the conversation line-split.
- Before mentioning or using any technology, website, reference, feature, algorithm, tool, or library, review its current authoritative source, then work from that (`laws/00-core.md`, Current sources). If the source cannot be reviewed, do not present the detail as current.
- Very strict: do not execute until required questions/checks complete, unless the user defers **for this time only**.
- Consuming project: every setting in laws `00`–`19`, template `PROJECT-SPECIFIC` bullets, and the project profile must be configured before product or code work (`laws/00-core.md` rules-setup gate). Hold the request until they are. Walk one section at a time and one unconfigured setting per turn. On an existing repo, write values the code already shows (database engine such as Firebase, Supabase, or SQL, and any other plain fact) and still ask for every setting the code does not prove. On a new repo, ask; do not invent facts. A blank, `not set`, or `_______________` is not configured.
- Every clarifying question: 1 question + 4 answers + option 5 custom blank; mark one **Recommended**; add short research hints when helpful.
- Ask always before build/start; during/after build only when ambiguous (unless deferred).
- New plans: brief CEO + HR + Sales discussion, then ask if another specialty is needed.
- Database laws always remain an awareness layer; determine DB type; mark `N/A` only after questioning.
- After every change: review modified elements, DB compatibility, logic/math, security, quality/structure.
- Minimal implementation (merged into laws, not a separate pack): after gates, use the `12` ladder (YAGNI → stdlib → native → installed dep → fewest lines); never cut validation/security/a11y/data-loss handling; intensity lite/full/ultra (default full).
- Complexity review tags + simplification debt ledger live in `13` / `16` (optional passes).
- Errors: show immediately + 4 solutions (one Recommended) + custom; **wait** before fixing; prefer root-cause.
- Existing projects: review → rethink → issue/fix plan → fixes (`16-existing-projects.md`).
- Product UI copy: prefer **conversational copy** — short, precise, formal (Arabic: فصحى, not dialect); use skill `.cursor/skills/conversational-copy/` and `laws/04-ux.md` voice rules.
- Branding / app icons: follow `17-branding-and-icons.md` when identity icons, favicons, launcher/PWA/store assets, or user-changeable icon packs are in scope.
- Security Laws suite (`10` + `18` + `19`): parent policy `10-security.md`; optional defensive scanners `18-security-tooling.md`; authorized discovery → remediation `19-vuln-discovery-and-remediation.md` (plan before fix; wait; no exploits).

## Do / Don’t

- DO fill PROJECT-SPECIFIC blanks in the consuming project when decisions are confirmed.
- DO mark modules `ACTIVE`, `N/A`, or keep `PROJECT-SPECIFIC` with notes.
- DON’T invent project facts in the public origin template.
- DON’T commit unless the user explicitly asks.

## Profile

Prefer filling `templates/project-profile.template.md` (or equivalent project copy) as the index of project truths.
