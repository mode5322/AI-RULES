---
name: git-checkpoint
description: Use before risky changes (many files, deletions, migrations, dependency updates, refactors) in a project that uses git. Checks repository state and proposes a safe checkpoint so the work can be rolled back.
---

# Git checkpoint

1. Run `git status`. If not a git repository, tell the user and continue without it.
2. If there are uncommitted changes, ask: commit them, stash them, or continue.
3. Propose a working branch name for non-trivial work (for example `feat/<short-name>`). Create it only after approval.
4. Never run `git reset --hard`, `git clean -fd`, force push, or delete branches without explicit approval.
5. Never commit secrets. If `.env` or keys appear in `git status`, warn and add to `.gitignore` after approval.
6. After the work passes `verify-and-fix`, suggest a commit message; commit only if the user agrees.
