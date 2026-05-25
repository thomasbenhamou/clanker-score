# Pattern 6 — Noise Filter Pattern

This is the detailed audit prompt for subagent 6. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 6 — Noise Filter Pattern

Check whether generated/vendor/build/cache/dependency directories are excluded from agent discovery/search where appropriate.

Investigation:

- Read `.claude/settings.json` if present.
- Read `.claude/settings.local.json` only for comparison; local-only config does not count as team setup.
- Look for `permissions.deny` rules that block reads/searches of noisy paths.
- Check for old/deprecated ignore-style config only as a signal, not as a full OK.
- Identify noisy directories that actually exist:
  - `node_modules/`
  - `dist/`
  - `build/`
  - `.next/`
  - `.nuxt/`
  - `coverage/`
  - `target/`
  - `vendor/`
  - `__pycache__/`
  - `.pytest_cache/`
  - `.mypy_cache/`
  - generated proto/openapi/graphql folders
  - generated SDK/client folders
  - large fixture or snapshot folders

Useful commands:

```bash
test -f .claude/settings.json && cat .claude/settings.json
test -f .claude/settings.local.json && cat .claude/settings.local.json
find . -maxdepth 4 -type d \( -name "node_modules" -o -name "dist" -o -name "build" -o -name ".next" -o -name ".nuxt" -o -name "coverage" -o -name "target" -o -name "vendor" -o -name "__pycache__" -o -name ".pytest_cache" -o -name ".mypy_cache" -o -iname "*generated*" \) -not -path "*/.git/*"
```

Verdict:

- **OK** if committed project config excludes the noisy paths that actually exist.
- **KO** if no committed config exists, exclusions only exist in `.local.json`, or major noise paths are uncovered.
- **OK with note** if the repo has no meaningful noisy/generated paths.

Remediation if KO:

- Provide an exact `.claude/settings.json` snippet using `permissions.deny`, tailored to paths found in the repo.

Example:

```json
{
  "permissions": {
    "deny": [
      "Read(./node_modules/**)",
      "Read(./dist/**)",
      "Read(./build/**)",
      "Read(./.next/**)",
      "Read(./coverage/**)",
      "Read(./vendor/**)"
    ]
  }
}
```

---

