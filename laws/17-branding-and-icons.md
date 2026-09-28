# 17 — Branding and Icons

## Purpose

Force explicit decisions for **project icons, app icons, and branding assets** across desktop, mobile, and web — including whether icons are **static** (shipped once) or **user-changeable** (settings / icon pack after ship). Prevent inventing icons, sizes, or folders without asking.

## Status

`ACTIVE | N/A | PROJECT-SPECIFIC` → default: `PROJECT-SPECIFIC`

Current: _______________

If `N/A`, reason: _______________

## When this module applies / when to skip

- Applies: any work that adds, replaces, relocates, or wires app/project icons, favicons, store listing icons, PWA icons, executable icons, or in-app branding marks used as the product identity.
- Applies when Settings (or similar) will let users pick an icon from a pack, or upload a custom icon.
- Lightweight apply: small UI iconography inside screens still follows `03-ui.md`; **product/app identity icons** stay under this module.
- `N/A` only after questioning confirms the project has **no** visual product identity surface (e.g. pure API/CLI with no installable shell, no web chrome, no store listing). Keep the file as a reminder if a shell may appear later.
- Cross-links: UI aesthetics → `03-ui.md`; changeable-icon UX → `04-ux.md`; asset folder layout → `05-architecture.md`; untrusted uploads / path safety → `10-security.md`.

## Hard rules (MUST / MUST NOT)

### Ask before inventing

- MUST NOT invent platform type, icon style, static vs changeable strategy, icon source, or required sizes when unknown.
- Before build/start of icon/branding work, MUST clarify via question protocol (platform(s), strategy, source, locations) unless PROFILE already records confirmed answers.
- During/after build: ask only when icon/branding choices are ambiguous.

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
- MUST ask which strategy applies before building Settings icon pickers or upload flows.
- For changeable icons: MUST define pack location, persistence key/store, fallback default, and whether custom uploads are allowed.
- MUST NOT treat UI glyph libraries (button icons) as the same decision as the **app identity** icon — keep them separate in PROFILE.

### Compatibility & security (high level)

- MUST keep branding decisions compatible with UI tokens and architecture folder rules (`03-ui.md`, `05-architecture.md`).
- If users can upload icons: MUST treat files as untrusted — validate type/size, sanitize paths, store outside executable rewrite paths, and avoid executing or interpreting uploads as code (`10-security.md`).
- MUST NOT write user-chosen icons to arbitrary filesystem paths from unsanitized input.
- Prefer contrast-safe defaults for light/dark shells when the product supports both.

### Module status

- Mark `N/A` only after questioning shows no identity/icon surface.
- When `N/A`, re-open this module if an installer, PWA, store listing, or branded shell appears later.

## Question protocol

Follow `templates/question-protocol.md`. Ask one question at a time.

### Example — Does this module apply?

```markdown
### Question
Does this project need product / app identity icons or branding assets?

1. Yes — installable or branded UI shell (desktop, mobile, and/or web) — **Recommended**
2. Yes — web only (favicon / PWA / touch icons)
3. Yes — in-app changeable icon pack in addition to launcher icons
4. No — API/CLI/backend only with no visual identity surface (candidate for N/A)
5. Other: _______________

Hints:
- Recommended when users will see a window, home-screen icon, browser tab icon, or store listing.
- To decide: check for `public/`, Electron/Tauri config, mobile `res/`, or PWA manifest.
```

### Example — Platform type(s)

```markdown
### Question
Which platform(s) must we deliver icons for?

1. Web / web app (favicon, apple-touch, PWA as needed) — **Recommended** if stack is web-first
2. Desktop application (.ico / .icns / packager icons)
3. Mobile application (adaptive + store sizes)
4. Multi-platform (specify combination in custom, or answer next)
5. Other: _______________

Hints:
- Recommended when the repo is primarily a website or SPA/PWA.
- To decide: inspect packagers, `manifest.json`, Android/iOS folders, Electron/Tauri config.
- Trade-off: multi-platform needs a master asset plus generated size sets per target.
```

### Example — Static vs changeable

```markdown
### Question
Should the product icon be static or user-changeable?

1. Static — one shipped default (and platform derivatives) — **Recommended**
2. Changeable — user picks from a built-in icon pack in Settings
3. Changeable — built-in pack + optional user upload
4. Build-time variants only (flavors/brands), not end-user Settings
5. Other: _______________

Hints:
- Recommended for most products; Settings icon packs add UX, storage, and security surface.
- To decide: check product requirements and whether competitors expose icon themes.
- Trade-off: uploads need validation and path safety; packs need persistence + default fallback.
```

### Example — Icon source / style

```markdown
### Question
Where should the identity icons come from?

1. Use existing project brand assets already in the repo — **Recommended** when present
2. User will provide master files (SVG/PNG) before implementation
3. Generate a simple placeholder set now; replace with final brand later
4. Licensed / third-party icon pack (name it in custom) for identity use
5. Other: _______________

Hints:
- Recommended whenever `branding/`, `assets/`, or design exports already exist.
- To decide: search the repo for favicon, `.icns`, `mipmap`, `AppIcon`, manifest icons.
```

### Example — Asset location

```markdown
### Question
Where should the source-of-truth icon set live?

1. `assets/icons/` (or `branding/icons/`) as master + toolchain exports — **Recommended**
2. Platform-native folders only (`public/`, `android/`, `ios/`, packager `build/`)
3. Design-system package shared across apps
4. Match existing repo convention (do not create a new root) — specify path in custom if known
5. Other: _______________

Hints:
- Recommended when you want one master set and generated platform derivatives.
- To decide: follow `05-architecture.md` PROFILE folder map; don’t fight a mature layout.
```

## New-project workflow

1. Confirm whether a visual identity surface exists; else mark `N/A` with reason.
2. Ask platform type(s), static vs changeable, icon source, and asset location.
3. Record answers in PROJECT-SPECIFIC and `templates/project-profile.template.md`.
4. Add master assets + required platform derivatives (favicon/PWA, desktop packager, mobile densities) before calling branding “done.”
5. If changeable: implement pack + Settings selection + persistence + default + accessibility; apply upload safety if uploads are allowed.
6. Cross-check UI (`03`), UX (`04`), architecture folders (`05`), and security (`10`).

## Existing-project workflow

1. Inventory current icons (favicon, manifest, launcher, `.ico`/`.icns`, store assets, Settings themes).
2. Detect whether icons are already user-changeable; do not add a pack without a product decision.
3. Prefer extending the existing asset location and naming; avoid a second parallel branding tree.
4. Treat missing platform sizes / broken favicons as defects when that platform is in scope.
5. Quick swap of a single file only if isolated; otherwise root-cause gaps in the size set or wiring (see `16-existing-projects.md`).
6. Update PROJECT-SPECIFIC with discovered truths (paths, default icon, strategy).

## Post-change checklist hooks

- [ ] Platform(s) and static vs changeable strategy confirmed or deferred once
- [ ] Assets live in the agreed location; source of truth documented
- [ ] Required sizes/formats for target platform(s) present or explicitly out of scope
- [ ] Default icon defined; changeable flow persists choice and falls back safely
- [ ] Uploads (if any) validated; paths safe; no trust of client filenames
- [ ] Compatible with UI/UX/architecture; no duplicate branding trees
- [ ] Module status still correct (ACTIVE / PROJECT-SPECIFIC / N/A)

## PROJECT-SPECIFIC

- Status: ACTIVE | N/A | PROJECT-SPECIFIC | _______________
- Platform type(s): desktop | mobile | web | multi: _______________
- Icon strategy: static | changeable-pack | changeable-pack+upload | build-time flavors | _______________
- Icon set location (source of truth): _______________
- Generated / platform export paths: _______________
- Default icon (filename or id): _______________
- Changeable pack ids / list path: _______________
- Persistence (key / store): _______________
- Upload allowed: yes | no — rules: _______________
- Master format: SVG | PNG | other: _______________
- Store / PWA / packager notes: _______________
- N/A rationale: _______________
