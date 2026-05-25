# Pattern 1 — Reproducible Development Environment Pattern

This is the detailed audit prompt for subagent 1. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 1 — Reproducible Development Environment Pattern

Check whether the repo can be installed, run, tested, and debugged from a clean checkout without relying on undocumented local machine setup.

Investigation:

- Look for reproducible setup files:
  - `.devcontainer/devcontainer.json`
  - `Dockerfile`
  - `docker-compose.yml`
  - `compose.yml`
  - `Makefile`
  - `justfile`
  - `mise.toml`
  - `.tool-versions`
  - `.nvmrc`
  - `.node-version`
  - `.python-version`
  - `.ruby-version`
  - `README.md`
  - `CLAUDE.md`
  - onboarding docs
- Check whether the repo documents:
  - prerequisites
  - install command
  - environment setup
  - local run command
  - test command
  - required services
  - database/bootstrap/migration steps
- Cross-check docs against actual repo files:
  - `package.json`
  - `pyproject.toml`
  - `composer.json`
  - `pom.xml`
  - `build.gradle`
  - `go.mod`
  - `Cargo.toml`
  - CI files

Useful commands:

```bash
find . -maxdepth 3 \( -name "devcontainer.json" -o -name "Dockerfile" -o -name "docker-compose.yml" -o -name "compose.yml" -o -name "Makefile" -o -name "justfile" -o -name "mise.toml" -o -name ".tool-versions" -o -name ".nvmrc" -o -name ".node-version" -o -name ".python-version" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
find . -maxdepth 3 \( -name "README.md" -o -name "CLAUDE.md" -o -iname "*onboarding*" -o -iname "*setup*" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
```

Verdict:

- **OK** if the repo has a clear, reproducible setup path and pinned or documented runtime requirements.
- **OK with note** if the repo is a tiny library/tool with trivial setup and the README is enough.
- **KO** if setup depends on undocumented local machine state, tribal knowledge, or missing commands.

Remediation if KO:

- Propose the minimum setup artifact to add:
  - `README.md` setup section
  - `CLAUDE.md` setup section
  - `.devcontainer/devcontainer.json`
  - `Makefile`
  - `justfile`
- Include concrete commands based on detected package managers and project files.

---

