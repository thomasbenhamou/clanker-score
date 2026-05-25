# Pattern 7 — Symbol Lookup Pattern

This is the detailed audit prompt for subagent 7. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 7 — Symbol Lookup Pattern

Check whether Language Server Protocol or code-intelligence capabilities are exposed to Claude through MCP or plugins.

Investigation:

- Read:
  - `.mcp.json`
  - `.claude/settings.json`
  - plugin config
  - docs mentioning LSP/code intelligence
- Look for LSP-related servers/plugins:
  - `serena`
  - `language-server`
  - `mcp-language-server`
  - `multilspy`
  - `typescript-lsp`
  - `pyright-lsp`
  - `php-lsp`
  - `java-lsp`
  - `gopls`
  - `rust-analyzer`
- Identify dominant languages by file count / repo files:
  - TypeScript / JavaScript
  - Python
  - PHP
  - Java
  - Go
  - C#
  - Rust

Useful commands:

```bash
test -f .mcp.json && cat .mcp.json
test -f .claude/settings.json && cat .claude/settings.json
find . -type f \( -name "*.ts" -o -name "*.tsx" -o -name "*.js" -o -name "*.jsx" -o -name "*.py" -o -name "*.php" -o -name "*.java" -o -name "*.go" -o -name "*.cs" -o -name "*.rs" \) -not -path "*/node_modules/*" -not -path "*/vendor/*" -not -path "*/.git/*" | sed 's/.*\.//' | sort | uniq -c | sort -nr
```

Verdict:

- **OK** if at least one LSP-backed MCP server or code-intelligence plugin is configured for the main language(s).
- **KO** if no symbol lookup tool is configured and the repo has strongly typed or large code.
- **OK with note** if the repo is tiny or has very low symbol collision risk.

Remediation if KO:

- Recommend `serena` MCP or matching official language plugin.
- Include install/config command if obvious.
- Mention which language(s) need coverage.

---

