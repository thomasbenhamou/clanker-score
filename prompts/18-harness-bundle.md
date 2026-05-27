# Pattern 18 — Harness Bundle Pattern

This is the detailed audit prompt for subagent 18. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 18 — Harness Bundle Pattern

Check whether skills, hooks, MCP config, agents, and repo guidance are packaged as a reusable bundle rather than one-off local config.

Investigation:

- Look for plugin/bundle manifests:
  - `plugin.json`
  - `marketplace.json`
  - `.claude-plugin/`
  - shared plugin documentation
- Check `.claude/settings.json` for:
  - `enabledPlugins`
  - shared plugin references
- Look for references to shared internal or external harnesses:
  - `anthropics/claude-plugins-official`
  - company/shared plugin repo
- Check whether the repo only has local `.claude/` content with no reuse path.

Useful commands:

```bash
find . -maxdepth 4 \( -name "plugin.json" -o -name "marketplace.json" -o -path "./.claude-plugin/*" -o -name "CLAUDE.md" -o -path "./.claude/*" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
test -f .claude/settings.json && cat .claude/settings.json
grep -RniE "enabledPlugins|plugin|marketplace|claude-plugins-official" . 2>/dev/null | head -100
```

Verdict:

- **OK** if a plugin/bundle exists or the team consumes a shared harness via plugin install.
- **KO** if skills/hooks/MCP/agents live only in this repo with no path to reuse.
- **OK with note** if the repo is intentionally standalone and no shared harness is expected.

Remediation if KO:

- Outline steps to extract the harness into a plugin.
- Provide a minimal structure:

```text
coding-agent-harness/
  plugin.json
  skills/
    verify-change/
      SKILL.md
  agents/
    security-reviewer.md
  hooks/
    post-edit-check.sh
  README.md
```

Minimal `plugin.json` template:

```json
{
  "name": "coding-agent-harness",
  "version": "0.1.0",
  "description": "Shared coding-agent setup: skills, hooks, agents, and verification workflows.",
  "author": "<team-or-org>",
  "skills": "./skills",
  "agents": "./agents",
  "hooks": "./hooks"
}
```

---

