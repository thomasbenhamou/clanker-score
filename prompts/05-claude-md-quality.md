# Pattern 5 — CLAUDE.md Quality Pattern

This is the detailed audit prompt for subagent 5. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 5 — CLAUDE.md Quality Pattern

Check whether root `CLAUDE.md` follows a quality rubric: includes what Claude cannot infer, excludes what it can infer by reading code.

Investigation:

- Read root `CLAUDE.md` if it exists.
- Check line count.
- Should include:
  - setup commands
  - test/lint/typecheck commands
  - repo-specific code style rules
  - architectural decisions specific to the project
  - environment quirks
  - required env vars without secret values
  - branch/PR conventions
  - common gotchas
  - non-obvious behavior
- Should not include:
  - generic “write clean code” platitudes
  - standard language conventions
  - file-by-file descriptions Claude can infer
  - long tutorials
  - detailed API docs that should be linked
  - duplicated README content
- Check whether it is stale or contradicts package/CI files.

Useful commands:

```bash
test -f CLAUDE.md && wc -l CLAUDE.md && sed -n '1,240p' CLAUDE.md
```

Verdict:

- **OK** if `CLAUDE.md` is concise, useful, repo-specific, and aligned with actual repo files.
- **KO** if missing, bloated, generic, stale, contradictory, or missing essentials like commands and gotchas.
- **OK with note** if a small repo has equivalent concise guidance in README and no separate `CLAUDE.md` is warranted.

Remediation if KO:

- List specific sections to delete or extract.
- List missing categories to add.
- Propose a compact replacement outline.

---

