# Project Profile Template

Configurable settings for a consuming project. Leave blanks empty on the public origin.

Ask each blank in the language the user is speaking. If the user answers in Arabic, store the value in English. The Arabic line-split in `laws/00-core.md` is fixed and is not a setting.

Laws `01`–`19` remain operating rules. They are not extra setup questions.

## Behavior

How the user deals with the agent.

- Conversation language: _______________
- Product UI language: _______________
- Rules-setup mode: strict-hold | configure-on-request | _______________

## System design

What the project is made of. On an existing repo, write values the code already shows, in English, and do not ask the user to re-confirm them.

- Database: none | Firebase | Supabase | SQL | _______________
- Framework: none | React | Flutter | React Native | _______________
- External connection: none | website | server | website and server | _______________
- External connection purpose: _______________
- Libraries in use: _______________

External connection purpose examples, stored in English: a website that only displays the product, or a server where the project database is created.

Libraries: the agent MUST keep using the libraries already in the project. Add a library only when the user asks for something those libraries do not provide. Then add the one library that provides it (for example icons). See `laws/12-code-quality.md`.
