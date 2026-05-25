# Pattern 9 — Deterministic Checks Pattern

This is the detailed audit prompt for subagent 9. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 9 — Deterministic Checks Pattern

Check whether quality checks run through hooks or repeatable commands rather than vague text instructions.

Investigation:

- Read `.claude/settings.json`.
- Look for `hooks`:
  - `PostToolUse`
  - `PreToolUse`
  - `Stop`
  - `UserPromptSubmit`
- Check matchers tied to editing tools:
  - `Edit`
  - `Write`
  - `MultiEdit`
- Cross-check hook commands against actual tools/scripts in:
  - `package.json`
  - `pyproject.toml`
  - `composer.json`
  - `Makefile`
  - `justfile`
  - `pom.xml`
  - `build.gradle`
  - `go.mod`
  - `Cargo.toml`
- Check whether hooks reference missing commands.

Useful commands:

```bash
test -f .claude/settings.json && cat .claude/settings.json
find . -maxdepth 3 \( -name "package.json" -o -name "pyproject.toml" -o -name "composer.json" -o -name "Makefile" -o -name "justfile" -o -name "pom.xml" -o -name "build.gradle" -o -name "go.mod" -o -name "Cargo.toml" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
```

Verdict:

- **OK** if hooks are configured to run actual project quality tools on file-edit events, or if equivalent deterministic commands are strongly documented for manual agent use.
- **KO** if no hooks/commands exist, hooks reference missing tools, or quality enforcement lives only as vague text.
- **OK with note** if repo is tiny and CI/commands are enough without hooks.

Remediation if KO:

- Provide a `.claude/settings.json` hook snippet referencing detected commands.
- Avoid inventing tools that do not exist in the repo.

Example shape:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write|MultiEdit",
        "hooks": [
          {
            "type": "command",
            "command": "npm run lint && npm run typecheck"
          }
        ]
      }
    ]
  }
}
```

---

