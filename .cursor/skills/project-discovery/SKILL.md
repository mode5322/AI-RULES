---
name: project-discovery
description: Use at the start of any task in a new or existing project, before writing code. Detects backend, database, language, framework and package manager from project files, records proven facts without asking, and asks only about missing information that the current task needs.
---

# Project discovery

## Workflow
1. Look for `.project/settings.md`. If present, trust its `set` values and skip detection for them.
2. Detect from files (read-only):
   - `package.json` (dependencies, scripts) -> Node.js, framework, test/lint/build commands
   - `composer.json`, `*.php`, `index.php` -> PHP
   - `pubspec.yaml` -> Dart / Flutter
   - `prisma/schema.prisma`, `drizzle.config.*`, `.env.example`, `docker-compose.yml`, `firebase.json`, `supabase/` -> database / backend
   - `requirements.txt`, `pyproject.toml`, `pom.xml`, `*.csproj`, `go.mod` -> other stacks
   - `electron`, `tauri`, `capacitor`, `react-native` in dependencies -> desktop / mobile target
3. Save what the code proves as `set` with source `detected`. Do not ask about it.
4. For missing facts the CURRENT task needs, ask using `project-settings/references/question-protocol.md`. Example: "Which backend: Node.js, Dart, PHP?"
5. Empty project: ask only the minimum to start (stack and language), nothing else.
6. Before using any library or tool API, check its current official docs. Do not rely on memory for versions or APIs.

## Do not
- Do not ask about design, security or other areas unrelated to the task.
- Do not guess the database from folder names alone. Ask if the code does not prove it.
