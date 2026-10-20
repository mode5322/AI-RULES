---
name: rtl-i18n
description: Use when the UI language is Arabic or another right-to-left language, when direction or UI language is unset for a new UI, or when mixed Arabic and English text appears. Sets direction, logical CSS, Arabic fonts, numerals and bidi handling.
---

# RTL and i18n

1. Read `ui_language`, `direction`, `numerals` from settings. If unset and the UI is user-facing, ask (question protocol): language, direction (rtl/ltr/both), numerals (Western 0-9 or Arabic-Indic).
2. Web: set `dir` and `lang` on `<html>`. Use CSS logical properties (`margin-inline-start`, `padding-inline-end`, `inset-inline-start`, `text-align: start`). With Tailwind use logical utilities or `rtl:` variants.
3. Flutter: use `Directionality` / locale; prefer `EdgeInsetsDirectional` and `AlignmentDirectional`.
4. Mirror icons that imply direction (arrows, back/next, progress). Do not mirror logos, clocks, media controls or numbers.
5. Fonts must support Arabic (for example Cairo, Tajawal, IBM Plex Sans Arabic, Noto Sans Arabic). Confirm availability in current docs. No letter-spacing on Arabic text; slightly larger line-height.
6. Mixed text: wrap embedded English, numbers or code in `<bdi>` or use `unicode-bidi: isolate`. Keep emails, URLs and code `dir="ltr"`.
7. Put all user-facing strings in a translation file; no hard-coded strings in components.
8. Verify visually in RTL: alignment, icon direction, form fields, tables, and truncated text.
