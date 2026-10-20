---
name: security-baseline
description: Use when the task involves authentication, forms, user input, database queries, file uploads, payments, API endpoints, secrets, or a desktop app shell (Electron). Applies a minimal security checklist for the area touched and asks only about security settings that block the task.
---

# Security baseline

Apply only the areas the task touches. Ask unset security settings (`auth_method`, `session_storage`) via the question protocol only when needed.

- **Passwords:** hash with a modern algorithm (Argon2id or bcrypt; PHP: `password_hash`). Never store or log plain text.
- **Database:** parameterized queries / prepared statements only (PHP: PDO). Never concatenate user input into SQL.
- **Input:** validate and sanitize on the server; client checks are only UX.
- **Output:** escape output to prevent XSS. Add CSRF protection for cookie sessions.
- **Sessions:** HttpOnly, Secure, SameSite cookies; rotate on login; expire on logout.
- **Login:** rate limit and generic error messages (do not reveal which field was wrong).
- **Secrets:** never in source code or committed `.env`; keep `.env.example` with placeholders.
- **Uploads:** check type and size, rename files, store outside web root.
- **Electron/desktop:** `contextIsolation` on, `nodeIntegration` off, expose a minimal preload API, validate IPC input.
- **Dependencies:** check the official docs for current secure usage before adding a package.

Report what was applied and any gap you could not close.
