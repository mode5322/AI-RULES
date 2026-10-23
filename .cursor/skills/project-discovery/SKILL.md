---
name: project-discovery
description: Use at the start of any task in a new or existing project, before writing code. Detects backend, database, language, framework and package manager from project files, records proven facts without asking, and asks only about missing information that the current task needs.
---

# Project discovery

## Workflow
1. Look for the project profile (**Behavior** and **System design**). If a value is already recorded, keep it.
2. Detect from files (read-only):
   - `package.json` (dependencies, scripts) -> Node.js, framework, test/lint/build commands
   - `composer.json`, `*.php`, `index.php` -> PHP
   - `pubspec.yaml` -> Dart / Flutter
   - `prisma/schema.prisma`, `drizzle.config.*`, `.env.example`, `docker-compose.yml`, `firebase.json`, `supabase/` -> database / backend
   - `requirements.txt`, `pyproject.toml`, `pom.xml`, `*.csproj`, `go.mod` -> other stacks
   - `electron`, `tauri`, `capacitor`, `react-native` in dependencies -> desktop / mobile target
3. Write a fact the code proves into the profile in English. Do not ask about it.
4. For a missing fact the current task needs, ask one question using `templates/question-protocol.md`. Do not ask when the task does not need that fact.
5. Empty project: record the conversation language from the user's message. Ask for a stack only when the request is to build an app and no stack exists. Ask nothing else.
6. Before using any library or tool API, check its current official docs. Do not rely on memory for versions or APIs.

## Do not
- Do not ask about design, security or other areas unrelated to the task.
- Do not guess the database from folder names alone. If the current task does not need a database and the repo has none, record `none` and do not ask. Ask only when the task needs a database and the code does not prove the engine.
