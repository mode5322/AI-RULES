# 11 — Change Management

## Purpose

Control how changes are planned, applied, reviewed, and rolled back so the project stays coherent.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `ACTIVE`


## When this module applies / when to skip

- Applies to every code or schema change.
- Lightweight for tiny copy fixes; full for schema, auth, payments, refactors.
- Works with `14-final-verification.md` and `16-existing-projects.md`.

## Hard rules (MUST / MUST NOT)

- MUST state the intent of a change before editing when the task is non-trivial.
- MUST make the smallest correct change.
- MUST apply the `12-code-quality.md` implementation ladder to the chosen approach (after gates).
- MUST NOT mix unrelated refactors into a bugfix.
- MUST assess blast radius: screens, services, DB, callers.
- MUST run the mandatory post-change review:
  1. Modified elements
  2. DB compatibility
  3. Logic/math
  4. Security/vulns
  5. Quality + structural compatibility
- MUST prefer root-cause fixes over temporary patches.
- MUST NOT use one-off migration hacks or single-run scripts as the durable fix when a proper path exists.
- Quick fix ONLY when there is **no project-wide impact**; otherwise plan a compatible root-cause fix.
- MUST NOT commit unless the user explicitly asks (agent rule).
- Schema/data changes require migration discipline from `06-database.md`.

## Upstream law merge

When a newer copy of this pack is brought into a consuming project, the entry is **Install and sync** («ثبّت وزامن») in `00-core.md` (copied folder, or repository URL). That command **always** includes this merge contract — first install or later update. Agents and reviewers MUST evaluate install-and-sync against these bullets; the user does not need a second special phrase.

- MUST NOT replace a configured setting with a blank, example, or placeholder from the public origin.
- MUST keep project-local rules and skills the user added that are not part of this pack. MUST NOT delete them when placing pack `.cursor/rules/` / `.cursor/skills/`.
- MUST delete obsolete **Behavior** and **System design** fields from the project profile when those fields are absent from the newer pack’s `templates/project-profile.template.md`. Retired upstream variables are removed; user-added non-pack rules are not profile fields and stay.
- MUST add new law files and new hard rules from the newer pack. Do not add a fill-in setting outside **Behavior** and **System design**.
- MUST apply rule text that the newer pack replaced. A configured profile value stays. It does not keep a deleted upstream rule alive unless that value is an explicit documented override, and **Law precedence** in `00-core.md` still applies.
- A new relevant Behavior or System design blank is unconfigured. Continue with **Resume in a new conversation** in `00-core.md`. Do not re-ask a configured setting, and do not ask a setting the project does not use.
- MUST state the source revision in the reply. Do not add a profile blank for it.
- MUST NOT push the filled project laws back to the public origin.

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Confirm requirements and discussion gates.
2. Choose change strategy if multiple approaches exist.
3. Implement smallest slice.
4. Run post-change review after each logical unit.
5. Verify with `14-final-verification.md`.

## Existing-project workflow

1. Map dependents before editing shared code.
2. Prefer compatible changes over breaking renames.
3. If a quick fix is requested but impact is wide, refuse the hack and propose root-cause options via error/solution protocol.
4. State a follow-up in the reply when the work is phased. Do not add a settings blank.

## Post-change checklist hooks

- [ ] Intent clear; scope minimal
- [ ] Blast radius assessed
- [ ] Five-point mandatory review done
- [ ] Rollback idea known for risky changes
- [ ] Install/sync merge: kept configured settings; kept user-added non-pack rules; removed obsolete profile fields; added new pack rules/blanks; recorded revision

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
