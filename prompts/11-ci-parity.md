# Pattern 11 — CI Parity Pattern

This is the detailed audit prompt for subagent 11. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 11 — CI Parity Pattern

Check whether local agent verification mirrors CI so agent-produced work does not pass locally but fail in the pipeline.

Investigation:

- Read CI config:
  - `.github/workflows/*`
  - `.gitlab-ci.yml`
  - `azure-pipelines.yml`
  - `bitbucket-pipelines.yml`
  - `circleci`
  - Jenkinsfile
- Extract CI commands:
  - install
  - lint
  - format
  - typecheck
  - test
  - build
  - security scan
- Compare with:
  - `CLAUDE.md`
  - README
  - hooks
  - skills
  - Makefile/justfile
- Identify CI-only checks missing from agent docs.

Useful commands:

```bash
find . -maxdepth 4 \( -path "./.github/workflows/*" -o -name ".gitlab-ci.yml" -o -name "azure-pipelines.yml" -o -name "bitbucket-pipelines.yml" -o -name "Jenkinsfile" -o -path "./.circleci/*" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
test -f CLAUDE.md && cat CLAUDE.md
test -f .claude/settings.json && cat .claude/settings.json
```

Verdict:

- **OK** if documented local checks match the meaningful CI checks.
- **KO** if CI has checks not documented for Claude, or Claude’s documented checks are weaker/stale.
- **OK with note** if there is no CI because the repo is tiny, archived, or documentation-only.

Remediation if KO:

- Add a `CI parity` or `Before PR` section to `CLAUDE.md`.
- Include exact CI-derived commands.
- Suggest adding a `make verify` or `just verify` wrapper if commands are complex.

---

