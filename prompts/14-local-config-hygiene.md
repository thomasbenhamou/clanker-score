# Pattern 14 — Local Config Hygiene Pattern

This is the detailed audit prompt for subagent 14. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 14 — Local Config Hygiene Pattern

Check whether AI-local config and secret files are properly git-ignored so personal config and secrets do not leak.

Investigation:

- Read:
  - `.gitignore`
  - `.git/info/exclude` if present
- Verify ignores include:
  - `CLAUDE.local.md`
  - `.claude/settings.local.json`
  - `.env`
  - `.env.*`
  - `.env.local`
  - `*.pem`
  - `*credentials*`
  - private key patterns
- Detect already tracked files that should not be tracked.

Useful commands:

```bash
test -f .gitignore && cat .gitignore
test -f .git/info/exclude && cat .git/info/exclude
git ls-files | grep -E '(^|/)(\.env$|\.env\.|CLAUDE\.local\.md$|settings\.local\.json$|.*\.pem$|.*credentials.*|id_rsa|id_ed25519)' || true
```

Verdict:

- **OK** if `.gitignore` excludes AI-local and secret patterns and no such files are tracked.
- **KO** if ignore entries are missing or sensitive/local files are already tracked.
- **OK with note** if the repo is not a git repo but still has safe local hygiene documented.

Remediation if KO:

- Provide exact `.gitignore` lines.
- If files are already tracked, provide exact commands:

```bash
git rm --cached <file>
```

Suggested `.gitignore` lines:

```gitignore
# Claude / AI local config
CLAUDE.local.md
.claude/settings.local.json

# Environment and secrets
.env
.env.*
!.env.example
*.pem
*credentials*
id_rsa
id_ed25519
```

---

