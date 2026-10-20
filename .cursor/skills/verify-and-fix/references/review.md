# Review the diff (two axes)

Review only the changes made in this task.

**Standards axis**
- Follows the project's existing structure, naming and style (and `GLOSSARY.md` terms).
- No dead code, duplicated logic, leftover logs, hard-coded secrets or magic values.
- Minimum code for the requirement; no speculative features.

**Spec axis**
- Does the change do exactly what the user asked? List anything missing and anything extra.

**UI audit (only if UI changed)**
- Keyboard navigation and visible focus.
- Contrast, labels, alt text, touch target size.
- Responsive at mobile width; RTL correct if direction is rtl.
- Uses saved colors, fonts and icon set only.

Report findings by severity. Fix blockers; list the rest for the user.
