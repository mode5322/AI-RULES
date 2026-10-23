# Usage playbook

Short guide for installing `strict-ai-rules` into a user project.

## Install

Two methods (`laws/00-core.md`, Install and sync). Copying or cloning alone does not fill the settings.

### Method 1

1. Copy the rules pack folder (the folder that contains `laws/`) into the consuming project root.
2. Tell the agent: «ثبّت وزامن القواعد من مجلد القواعد على المشروع الحالي».

### Method 2

Send the repository URL and the command in one message:

> ثبّت وزامن قواعد هذا المستودع مع المشروع الحالي
> https://github.com/mode5322/strict-ai-rules

The agent places `laws/` and `templates/` at the project root and writes **Behavior** and **System design** from the current project. Unused parts are `none` and are not asked.

## After sync

1. A relevant field the code does not show, and that this request needs, is asked once, in the user’s language. An Arabic answer is stored in English.
2. The held request then proceeds.
3. Laws `01`–`19` open when the task needs that file. They are not the setup walk.

## New project flow

1. Install and sync first.
2. Ask one question only when the request needs a fact the repo does not show.
3. Implement after that question is answered, or after a one-time deferral.
4. After each change: five-point review, then `14-final-verification.md`.

## Existing project flow

1. Rules-setup gate first (`00`), by **Install and sync**. Code-backed facts are written during that sync.
2. Then start at `16-existing-projects.md` (+ `13-ai-review.md`).
3. Audit → rethink → issue/fix plan → confirm → fix.
4. Quick fix only when impact is isolated; otherwise root-cause with compatibility.
5. Security Laws suite: optional scanners `18-security-tooling.md` under parent `10`; actionable vulns via `19-vuln-discovery-and-remediation.md` (plan before fix; wait).

## Deferral

To skip questions once, or to skip rules setup for the current task only, say clearly you defer **for this time only** (see `templates/deferral.md`). Strict mode returns afterward. The agent holding the first request for rules setup is not this deferral.

To **stop the rules-setup question walk** until you later ask to configure the rules, say: **Stop the question protocol until I ask to configure the rules** (Arabic fixed title: «إيقاف بروتوكول الأسئلة إلى أن أطلب ضبط إعدادات القواعد»). That sets mode `configure-on-request`. These phrases are commands, not settings the agent asks about (`templates/deferral.md`).

The option list appears only when a decision is necessary and you say «عرض خيارات» or "Show options".

To **show incomplete rule settings**, ask for them. The agent numbers every **relevant** remaining setting from 1 through the full count, then shows a category table of completed and remaining. Unrelated blanks stay hidden unless you ask to see them (`laws/00-core.md`).

## Keeping the origin clean

Do not push your project-specific filled laws back to the public `strict-ai-rules` origin. Customize only in your project copy.

## Updating from upstream

When a newer pack is copied onto a project that already has filled settings, follow `laws/11-change-management.md` (Upstream law merge):

1. Keep every configured value. Do not paste origin blanks over them.
2. Add new laws and new blank settings from the newer pack.
3. Continue setup only for the new blanks (`laws/00-core.md`, Resume in a new conversation).
4. Record the upstream revision in the project profile.
5. Do not push the filled result back to the public origin.
