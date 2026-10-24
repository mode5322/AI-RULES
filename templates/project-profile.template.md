# Project Profile Template

Configurable settings for a consuming project. Leave blanks empty on the public origin.

Ask a blank in the language the user is speaking, and only when that blank connects to the current project. If the user answers in Arabic, store the value in English. If the project does not use that part, record `none` and do not ask. Show an unrelated blank only when the user asks to see or configure it. The mixed-script bidi rules in `laws/00-core.md` are fixed and are not a setting.

Laws `01`–`19` remain operating rules. They are not extra setup questions.

## Behavior

How the user deals with the agent.

- Conversation language: _______________
- Rules-setup mode: strict-hold | configure-on-request | _______________

Do not ask the mode. A blank means `strict-hold`. Ask only when the user asks to change it.

## System design

What the project is made of. On an existing repo, write values the code already shows, in English, and do not ask the user to re-confirm them. If the project does not use a part, record `none` and do not ask.

- Database: none | Firebase | Supabase | SQL | _______________
- Framework: none | React | Flutter | React Native | _______________
- External connection: none | website | server | website and server | _______________
- External connection purpose: _______________
- Libraries in use: _______________
- UI components: _______________

When the user designs a button, a form, or a screen, record that component in English under **UI components** and build it once. What changes between uses (label, action, state) is an input, so the same component is reused. Do not copy the element for each screen. If the repo already has the component, reuse it and do not ask. If the project has no interface, record `none`.

External connection purpose examples, stored in English: a website that only displays the product, or a server where the project database is created.

Libraries: the agent MUST keep using the libraries already in the project. Add a library only when the user asks for something those libraries do not provide. Then add the one library that provides it (for example icons). See `laws/12-code-quality.md`.
