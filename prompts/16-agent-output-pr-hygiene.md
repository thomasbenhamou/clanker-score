# Pattern 16 — Agent Output / PR Hygiene Pattern

This is the detailed audit prompt for subagent 16. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 16 — Agent Output / PR Hygiene Pattern

Check whether the repo defines how coding agents should summarize changes, structure PRs/MRs, list tests run, and expose risks.

Investigation:

- Look for:
  - `.github/PULL_REQUEST_TEMPLATE.md`
  - `.gitlab/merge_request_templates/`
  - `CONTRIBUTING.md`
  - `CLAUDE.md`
  - commit conventions
  - changelog rules
  - branch naming rules
  - release note rules
- Check whether agents are told to include:
  - summary of changes
  - why change was made
  - tests run
  - risks
  - rollback considerations
  - screenshots for UI changes
  - migration notes
  - config/env changes
- Check whether attribution policy is intentional:
  - whether Claude-generated commits/PRs should include attribution
  - whether team policy says not to include it

Useful commands:

```bash
find . -maxdepth 4 \( -name "PULL_REQUEST_TEMPLATE.md" -o -path "./.github/PULL_REQUEST_TEMPLATE/*" -o -path "./.gitlab/merge_request_templates/*" -o -name "CONTRIBUTING.md" -o -name "CLAUDE.md" -o -name "CHANGELOG.md" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
test -f CLAUDE.md && grep -niE "pull request|merge request|PR|MR|commit|changelog|tests run|risk|rollback|screenshot|attribution" CLAUDE.md
```

Verdict:

- **OK** if the repo defines useful PR/MR output expectations for agents.
- **KO** if PR output is unconstrained and agents would improvise summaries.
- **OK with note** if the repo is not intended for PR/MR-based collaboration.

Remediation if KO:

- Propose a PR/MR template or `CLAUDE.md` section.

Example:

```md
## PR / MR output

When preparing a change summary, include:

- Summary: 2–4 bullets describing what changed.
- Verification: exact commands run and whether they passed.
- Risk: migration, config, data, security, or compatibility risks.
- Screenshots: required for UI changes.
- Rollback: note if rollback is non-trivial.
```

---

