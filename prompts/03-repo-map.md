# Pattern 3 — Repo Map Pattern

This is the detailed audit prompt for subagent 3. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 3 — Repo Map Pattern

Check whether a lightweight repo map exists at the root: a markdown file listing top-level folders with one-line descriptions.

Investigation:

- Look for:
  - `REPO_MAP.md`
  - `ARCHITECTURE.md`
  - `STRUCTURE.md`
  - `PROJECT_STRUCTURE.md`
  - `MAP.md`
  - a clearly labelled section in `README.md`
  - a clearly labelled section in root `CLAUDE.md`
- Verify the file lists most top-level directories with at least:
  - folder name
  - one-line purpose
- Cross-check coverage against actual top-level directories.

Useful commands:

```bash
ls -d */ 2>/dev/null
find . -maxdepth 2 \( -name "REPO_MAP.md" -o -name "ARCHITECTURE.md" -o -name "STRUCTURE.md" -o -name "PROJECT_STRUCTURE.md" -o -name "MAP.md" -o -name "README.md" -o -name "CLAUDE.md" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
```

Verdict:

- **OK** if a factual map exists and covers most top-level folders.
- **KO** if no map exists, the map is stale, most folders are missing, or it is narrative prose without folder mapping.
- **OK with note** if the repo is tiny and the top-level structure is self-evident.

Remediation if KO:

- Propose a root `REPO_MAP.md`.
- Include the actual folder list from `ls -d */`.
- Suggest this format:

```md
# Repo Map

| Folder | Owner | Purpose | Main entry point |
|---|---|---|---|
| `apps/foo/` | Team/name if known | One-line purpose | `apps/foo/src/...` |
```

---

