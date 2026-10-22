---
name: conversational-copy
description: >-
  Writes short, precise product UI copy in formal register (Arabic: Modern
  Standard Arabic / fusHa). Use when drafting or editing labels, buttons,
  settings cards, empty states, errors, confirms, tooltips, in-app notices, or
  when the user asks for human tone, shorter text, formal Arabic, or to avoid
  AI-sounding fluff or dialect.
---

# Conversational copy

Canonical name: **conversational copy**. Also: human concise voice. For short UI strings: microcopy.

## Goal

User-facing text that is **short**, **precise**, and **human** — written like clear staff instructions, not a brochure, not an AI essay, and not slang chat.

## Register (language)

1. Match the product language.
2. For **Arabic** product UI: use **Modern Standard Arabic (فصحى)** only.
3. MUST NOT use dialect or colloquial fillers (examples to avoid: «لحظات…»، «صار خطأ»، «تحوّلها»، «نكمّل؟» as the sole CTA).
4. Prefer careful, standard wording (examples: «يرجى الانتظار»، «حدث خطأ غير متوقع»، «تحويل العملية للأجل ؟»).

## Rules

1. Prefer the shortest **clear** line. Cut filler and AI padding — without sacrificing correctness or formality.
2. One idea per sentence. No stacked marketing clauses.
3. Keep versions, paths, and code tokens isolated (`dir="ltr"` / `<bdi>` when needed).
4. Buttons: one coherent action. Do not glue unrelated verbs in one label (bad: «أوافق وأدخل» → good: «أوافق»).
5. Do not duplicate a question inside the button when the dialog already asks it.
6. Errors / empty / loading: clear formal phrasing — what happened + what to do when needed. No apology essays. No slang.
7. Copy MUST match the UI that exists now. MUST NOT describe removed features or leftover copy from older versions.
8. Avoid buzzwords, triple adjectives, rhetorical padding, redundant card CTAs («فتح الإعداد»، «فتح القسم»), and decorative emoji in copy.

## Checklist

- [ ] Is it فصحى (if Arabic), not dialect?
- [ ] Would a careful human write this as a product instruction?
- [ ] Can any word be deleted without losing meaning or correctness?
- [ ] Does every claim match the current UI?
- [ ] Does the button label contain only one coherent action?

## Examples

| Bad | Good |
|---|---|
| يتم الاتصال بخادم التحديثات للتحقق من وجود إصدار أحدث. | جاري البحث عن تحديثات. |
| لحظات... | يرجى الانتظار |
| صار خطأ | حدث خطأ غير متوقع |
| أوافق وأدخل | أوافق |
| تحوّلها لأجل؟ | تحويل العملية للأجل ؟ |
| لا إعدادات تلغرام — اربط البوت أولاً. | لم يتم ضبط إعدادات التلغرام، يرجى إضافة إعدادات البوت أولاً. |
| فتح الإعداد / فتح القسم (on a whole-card button) | omit — the card is enough |
| وصف يذكر «أقسام محددة» بينما الواجهة نسخة شاملة فقط | وصف يطابق الأزرار الموجودة فعلاً |
| تنظيم بسيط حسب المهام وسهولة الوصول | اختر ما تريد تعديله |
