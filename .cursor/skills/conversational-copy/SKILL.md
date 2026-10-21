---
name: conversational-copy
description: >-
  Writes short, natural product UI copy (conversational copy / human concise
  voice / microcopy). Use when drafting or editing labels, buttons, settings
  cards, empty states, errors, confirms, tooltips, in-app notices, or when the
  user asks for human tone, shorter text, or to avoid AI-sounding fluff.
---

# Conversational copy

Canonical name: **conversational copy**. Also: human concise voice. For short UI strings: microcopy.

## Goal

User-facing text that is short, spoken, and human — not padded, not corporate, not essay-like.

## Rules

1. Prefer the shortest clear line. Cut filler.
2. Sound like a person talking to a shop worker, not a brochure.
3. One idea per sentence. No stacked clauses.
4. Match the product language. Keep versions, paths, and code tokens isolated (`dir="ltr"` / `<bdi>` when needed).
5. Buttons: verb (+ object if needed). Do not duplicate the question in the button.
6. Errors: what happened + what to do. No apology essays.
7. Do not invent features in the copy. Do not over-explain what the UI already shows.
8. Avoid buzzwords, triple adjectives, rhetorical padding, and decorative emoji in copy.

## Checklist

- [ ] Would a human say this out loud?
- [ ] Can any word be deleted without losing meaning?
- [ ] Does it sound like a person, not a template?

## Examples

| Bad | Good |
|---|---|
| يتم الاتصال بخادم التحديثات للتحقق من وجود إصدار أحدث. | نبحث عن إصدار أحدث. |
| فتح الإعداد (on a whole-card button) | omit — the card is enough |
| هل تريد تثبيت التحديث؟ + نعم، ثبّت التحديث | ثبّت التحديث |
| تنظيم بسيط حسب المهام وسهولة الوصول | اختر ما تريد تعديله |
