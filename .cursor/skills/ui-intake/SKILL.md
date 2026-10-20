---
name: ui-intake
description: Use whenever the user asks for any user interface (page, screen, component, form, dashboard, login page). Asks about visual style, icons, colors and fonts only if unset, saves answers, then builds a distinctive, accessible UI. Never uses emoji as icons.
---

# UI intake

## Workflow
1. Read `.project/settings.md` (create via project-settings if missing).
2. Ask ONLY the unset Design settings relevant to this UI (see protocol in `project-settings/references/question-protocol.md`):
   - `ui_style`: options in `references/styles.md`
   - `icon_library`: options in `references/icons.md`
   - colors, fonts, radius, dark mode
3. If the UI language is Arabic or direction is unset, also apply the `rtl-i18n` skill.
4. Build the UI with the saved settings. Quality bar:
   - Intentional typography and spacing; avoid generic template look.
   - All states: hover, focus-visible, disabled, loading, empty, error.
   - Responsive from mobile width. Sufficient color contrast. Labels on inputs. Keyboard usable.
   - One consistent icon set. Colors and fonts from settings, never hard-coded ad hoc.
5. Hand over to `verify-and-fix`.

## Hard rule
Never use emoji or keyboard characters as icons. Use the chosen icon library (SVG).
