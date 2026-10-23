---
name: ui-intake
description: Use whenever the user asks for any user interface (page, screen, component, form, dashboard, login page). Match the existing UI. Ask one question only when the screen cannot be built from it. Never uses emoji as icons.
---

# UI intake

## Workflow
1. Read the existing UI. Do not create `.project/settings.md` and do not ask for colors, fonts, radius, or an icon library.
2. Use the installed icon library. Add one only when the user asks for an icon the installed libraries do not provide.
3. If the UI language is Arabic, apply the `rtl-i18n` skill. Do not ask for direction when the language is already Arabic.
4. Apply the `conversational-copy` skill for all user-facing strings (labels, buttons, empty/error/success, confirms).
5. Build the UI from the existing product. Quality bar:
   - Intentional typography and spacing; avoid generic template look.
   - All states: hover, focus-visible, disabled, loading, empty, error.
   - Responsive from mobile width. Sufficient color contrast. Labels on inputs. Keyboard usable.
   - One consistent icon set already in the project. Match existing colors and fonts.
6. Hand over to `verify-and-fix`.

## Hard rule
Never use emoji or keyboard characters as icons. Use an installed icon library (SVG). Add one only when the user asks for an icon the installed libraries do not provide.
