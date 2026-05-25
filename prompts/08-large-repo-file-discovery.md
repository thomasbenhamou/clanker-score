# Pattern 8 — Large-Repo File Discovery Pattern

This is the detailed audit prompt for subagent 8. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 8 — Large-Repo File Discovery Pattern

Check whether large repos provide fast file discovery/indexing so agents do not rely only on blind grep/find.

Investigation:

- Estimate repo size:
  - number of files
  - number of top-level packages/apps/services
  - monorepo indicators
- Look for:
  - `REPO_MAP.md`
  - `.claude/settings.json` `fileSuggestion`
  - generated repo index
  - `ctags`
  - sourcegraph/docs
  - architecture index
  - package ownership map
  - workspace manifests
  - `pnpm-workspace.yaml`
  - `nx.json`
  - `turbo.json`
  - `lerna.json`
- Check whether `CLAUDE.md` tells agents how to find files efficiently.

Useful commands:

```bash
git ls-files | wc -l
ls -d */ 2>/dev/null
find . -maxdepth 3 \( -name "pnpm-workspace.yaml" -o -name "nx.json" -o -name "turbo.json" -o -name "lerna.json" -o -name "REPO_MAP.md" -o -name "ARCHITECTURE.md" -o -name "CLAUDE.md" -o -name "settings.json" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
test -f .claude/settings.json && cat .claude/settings.json
```

Verdict:

- **OK** if a large repo has custom file discovery, repo map, workspace map, or file suggestion config.
- **OK with note** if small repo.
- **KO** if a large repo relies only on ad hoc `grep`/`find` with no map or discovery guidance.

Remediation if KO:

- Propose `REPO_MAP.md`.
- Propose a `fileSuggestion` config if appropriate.
- Propose a command section in `CLAUDE.md` for fast search.

---

