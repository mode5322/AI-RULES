---
name: problem-brief
description: >-
  Explains a diagnosed problem in a short fixed Arabic brief when the user asks
  what went wrong and clearly does not know the cause. Use for runtime failures,
  500s, missing files, wrong paths, misconfigured env, and similar investigation
  results before offering fix choices.
---

# Problem brief

When the user asks about a failure or odd behavior and **does not already know the cause**, answer first with this short brief — then, if a fix is needed, continue with the error-handling solutions protocol (`laws/15-error-handling.md`).

## Format (exact labels)

Emit as **bare paragraphs** in the chat reply. MUST NOT wrap the brief in a fenced code block (triple backticks), `<pre>`, monospace dump box, or any UI box with a border/copy chip. Those boxes reverse Arabic+Latin in common chat viewers.

When the conversation is Arabic/RTL, apply Behavior → `Arabic mixed-script display` (`laws/00-core.md`) on **every** brief line (U+200F / LRI / backticks as required by the stored method). Latin paths and filenames stay isolated per that method; do not leave them bare inside Arabic lines.

مكان المشكلة = <path or URL where the failure appears>
سبب المشكلة = ملف (<filename>), <short cause>
حل المشكلة = <primary fix: move/copy/create what → where>
حل المشكلة بطريقة أخرى = يجب تعديل <what> في الملف "<file path>" في السطر رقم "<N>"
يجب أن يكون "<exact expected line, value, or shape>"

## Rules

1. Keep each line short. Formal Arabic (فصحى) for explanations; paths and filenames use the active mixed-script method.
2. Name the real file that fails (not a vague “السيرفر”).
3. Primary fix = safest root-cause action (e.g. put the missing file in the path the code expects).
4. Alternate fix = code/config change with **file path + line number + exact expected form**.
5. Do not dump long logs in the brief. Put evidence after the brief only if useful — also as bare paragraphs when Arabic, not a second code box for mixed prose.
6. Do not invent causes. If still unknown, say so and list what was checked — then ask with question protocol.
7. When the user already knows the cause and only wants a fix, skip this brief and go to solutions.

## Example (bare paragraphs; marks depend on stored method)

مكان المشكلة = https://pos.cscorse.com/api_admin99532_pos/v1/auth/login.php
سبب المشكلة = ملف (cfg_enkidu_7k2m.php)، خطأ في مسار ملف .env
حل المشكلة = وضع ملف ".env" في المسار التالي "pos.cscorse.com/.env"
حل المشكلة بطريقة أخرى = يجب تعديل المسار في الملف "api_admin99532_pos/cfg_enkidu_7k2m.php" في السطر رقم "4"
يجب أن يكون "$serverRoot = dirname(__DIR__, 2);"  (أو مسار ثابت لجذر الحساب حيث يوجد .env)
