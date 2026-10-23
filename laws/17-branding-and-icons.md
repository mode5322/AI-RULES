# 17 — Branding and Icons

## Purpose

Force explicit decisions for **project icons, app icons, and branding assets** across desktop, mobile, and web — including whether icons are **static** (shipped once) or **user-changeable** (settings / icon pack after ship). Prevent inventing icons, sizes, or folders without asking.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`



## When this module applies / when to skip

- Applies: any work that adds, replaces, relocates, or wires app/project icons, favicons, store listing icons, PWA icons, executable icons, or in-app branding marks used as the product identity.
- Applies when Settings (or similar) will let users pick an icon from a pack, or upload a custom icon.
- Lightweight apply: small UI iconography inside screens still follows `03-ui.md`; **product/app identity icons** stay under this module.
- Skip this file when the project has no app icon, favicon, store listing, or branded shell. Do not ask to confirm that absence. Re-open the file if that surface appears later.
- Cross-links: UI aesthetics → `03-ui.md`; changeable-icon UX → `04-ux.md`; asset folder layout → `05-architecture.md`; untrusted uploads / path safety → `10-security.md`.

## Hard rules (MUST / MUST NOT)

### Ask before inventing

- MUST NOT invent platform type, icon style, or sizes.
- When the current task is icon or branding work and the repo does not show the platform, ask one question. Otherwise do not open this module.

### Platform-specific deliverables

When the platform applies, MUST plan for the correct asset classes (adapt to stack/tooling; do not invent vendor-specific paths without checking the project):

| Platform | Typical requirements (ask / verify; do not skip silently) |
|---|---|
| **Desktop** | Window/app icon; Windows `.ico` (multi-size); macOS `.icns` or platform-equivalent; Linux PNG/SVG where used; installer / executable icon embedding when the packager requires it |
| **Mobile** | Adaptive / round / legacy launcher icons; density/size set for the target OS; splash / store listing artwork when shipping to stores; safe-zone awareness for adaptive masks |
| **Web / PWA** | Favicon set (e.g. ICO/PNG/SVG); `apple-touch-icon`; PWA / web app manifest icons (multiple sizes); theme-color / maskable icons when PWA |

- MUST NOT ship a single arbitrary PNG and claim “done” for store, OS, or PWA requirements when the platform needs a size set.
- MUST match existing brand marks when the project already has them — do not redesign without an explicit decision.

### Project structure

- MUST place icon / branding assets in the project’s agreed location (see PROJECT-SPECIFIC / architecture), not scattered one-offs across unrelated folders.
- Suggested roles (adapt names to stack): `assets/icons/` or `branding/` for identity; platform-generated exports (e.g. `android/`, `ios/`, `public/`, Electron `build/`) stay where the toolchain expects them.
- MUST document the **source of truth** icon (master SVG/PNG) vs generated derivatives when both exist.
- MUST NOT commit huge unused export dumps without a clear generation/source story.

### Static vs user-changeable

- **Static**: one default (or build-time) product icon; users cannot change the app/launcher identity in Settings.
- **Changeable**: app ships with an **icon pack** (and/or allows upload); user selects in Settings; choice is **persisted**; default icon is defined; UI must remain accessible (labels, contrast, not icon-only critical actions — see `04-ux.md`).
- If the user asked for a settings icon picker or upload, the strategy is changeable. If they asked only for a fixed app icon or favicon, the strategy is static. Ask one question only when the request says neither.
- For changeable icons: MUST define pack location, persistence key/store, fallback default, and whether custom uploads are allowed.
- MUST NOT treat a UI glyph library as the app identity icon. Use an installed library for glyphs. Add a library only when the user asks for an icon the installed libraries do not provide.

### Compatibility & security (high level)

- MUST keep branding decisions compatible with UI tokens and architecture folder rules (`03-ui.md`, `05-architecture.md`).
- If users can upload icons: MUST treat files as untrusted — validate type/size, sanitize paths, store outside executable rewrite paths, and avoid executing or interpreting uploads as code (`10-security.md`).
- MUST NOT write user-chosen icons to arbitrary filesystem paths from unsanitized input.
- Prefer contrast-safe defaults for light/dark shells when the product supports both.

### Module status

- Skip this file when the project has no identity-icon surface. Do not ask.
- When `N/A`, re-open this module if an installer, PWA, store listing, or branded shell appears later.

## Question protocol

Ask from this file only when the current task needs this module and the repo does not already show the answer. Follow `templates/question-protocol.md`: one short line in the user's language, and the option list only after «عرض خيارات» or "Show options". Store an Arabic answer in English. Do not add a fill-in setting in this file.

## New-project workflow

1. Use this file only when the current task is identity-icon work.
2. Read the platform from the repo. Ask one question only when the request does not say whether the icon is fixed or changeable.
3. Put assets next to the project's existing asset folder.
4. Add the platform sizes the current target actually requires before calling branding done.
5. If the icon is changeable: pack, selection, persistence, default, and upload checks when upload is requested.
6. Cross-check UI (`03`), UX (`04`), architecture folders (`05`), and security (`10`).

## Existing-project workflow

1. Inventory current icons (favicon, manifest, launcher, `.ico`/`.icns`, store assets, Settings themes).
2. Detect whether icons are already user-changeable; do not add a pack without a product decision.
3. Prefer extending the existing asset location and naming; avoid a second parallel branding tree.
4. Treat missing platform sizes / broken favicons as defects when that platform is in scope.
5. Quick swap of a single file only if isolated; otherwise root-cause gaps in the size set or wiring (see `16-existing-projects.md`).
6. Do not add a settings blank for the path.

## Post-change checklist hooks

- [ ] This task was identity-icon work, or the file was left unused
- [ ] Assets live beside the existing asset folder
- [ ] Required sizes/formats for target platform(s) present or explicitly out of scope
- [ ] Default icon defined; changeable flow persists choice and falls back safely
- [ ] Uploads (if any) validated; paths safe; no trust of client filenames
- [ ] Compatible with UI/UX/architecture; no duplicate branding trees
- [ ] Module left unused when the project has no identity icon

## PROJECT-SPECIFIC

No fill-in settings live here. Behavior and System design are only in `templates/project-profile.template.md`. If this module does not connect to the current project, do not ask about it.
