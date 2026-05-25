# Pattern 4 — Context Cascade Pattern

This is the detailed audit prompt for subagent 4. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 4 — Context Cascade Pattern

Check whether `CLAUDE.md` files are layered across the tree, not concentrated in a single bloated root file.

Investigation:

- Find all `CLAUDE.md` files.
- For each file:
  - line count
  - location
  - approximate scope
  - whether it contains global or local guidance
- Identify whether the root file is bloated:
  - more than 200 lines
  - mixes global + local + workflow + team-specific details
  - repeats code-derivable information
- Identify whether subtree files hold local commands, conventions, domain terms, or gotchas.

Useful commands:

```bash
find . -name "CLAUDE.md" -type f -not -path "*/node_modules/*" -not -path "*/.git/*" -not -path "*/dist/*" -not -path "*/build/*"
find . -name "CLAUDE.md" -type f -not -path "*/node_modules/*" -not -path "*/.git/*" -exec wc -l {} +
```

Verdict:

- **OK** if there are multiple `CLAUDE.md` files at different depths and the root stays focused on global rules while subtree files hold local concerns.
- **OK with note** if the repo is a small single-domain project where cascade adds no value.
- **KO** if there is no `CLAUDE.md`, only a bloated root file, or subtree files duplicate global rules.

Remediation if KO:

- List specific subtrees that should receive their own `CLAUDE.md`.
- List root sections that should be extracted into subtree files.
- Suggest a concise root structure:

```md
# CLAUDE.md

## Purpose
## Setup
## Commands
## Verification
## Architecture constraints
## Repo conventions
## Gotchas
```

---

