# Pattern 10 — Verifiable Work Loop Pattern

This is the detailed audit prompt for subagent 10. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 10 — Verifiable Work Loop Pattern

Check whether the repo gives Claude exact commands to verify its own work without human intervention.

Investigation:

- Read:
  - root `CLAUDE.md`
  - README
  - relevant skills
  - Makefile/justfile
- Look for sections:
  - “Verification”
  - “Testing”
  - “How to check”
  - “Bash commands”
  - “Before submitting”
- Check whether specific commands are listed:
  - test
  - lint
  - typecheck
  - build
  - focused tests
  - screenshot/UI checks
- Cross-check against actual scripts.

Useful commands:

```bash
test -f CLAUDE.md && grep -niE "verification|testing|test|lint|typecheck|build|check|commands|before submitting" CLAUDE.md
test -f README.md && grep -niE "verification|testing|test|lint|typecheck|build|check|commands" README.md
find . -maxdepth 3 \( -name "package.json" -o -name "pyproject.toml" -o -name "composer.json" -o -name "Makefile" -o -name "justfile" -o -name "pom.xml" -o -name "build.gradle" -o -name "go.mod" -o -name "Cargo.toml" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
```

Verdict:

- **OK** if Claude has exact verification commands and they match actual repo scripts/tools.
- **KO** if no verification commands are documented, commands are stale, or commands do not match repo files.
- **OK with note** if the repo is documentation-only or otherwise has no executable verification.

Remediation if KO:

- List actual detected commands.
- Propose a `CLAUDE.md` section:

```md
## Verification

Before finishing a code change, run:

- Install: `<command>`
- Lint: `<command>`
- Typecheck: `<command>`
- Unit tests: `<command>`
- Focused test: `<command>`
- Build: `<command>`
```

---

