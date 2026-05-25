# Pattern 15 — Just-in-Time Skill Pattern

This is the detailed audit prompt for subagent 15. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 15 — Just-in-Time Skill Pattern

Check whether specialized workflows are packaged as skills loaded on demand rather than dumped into `CLAUDE.md`.

Investigation:

- List skills:
  - `.claude/skills/`
  - subtree `.claude/skills/`
- For each skill:
  - read `SKILL.md`
  - verify frontmatter has a clear `description`
  - verify skill is narrow and task-specific
- Check root `CLAUDE.md` for huge task-specific workflow sections that should be skills:
  - security review
  - deployment
  - migration
  - release
  - code review
  - test strategy
  - observability/debugging
  - data fixes
- Check whether recurring workflows are still in `.claude/commands/`; this is acceptable, but skills are preferred for new setup.

Useful commands:

```bash
find . -path "*/.claude/skills/*/SKILL.md" -type f -not -path "*/node_modules/*" -not -path "*/.git/*"
find . -path "*/.claude/commands/*" -type f -not -path "*/node_modules/*" -not -path "*/.git/*"
test -f CLAUDE.md && wc -l CLAUDE.md && grep -niE "deploy|release|migration|security|review|observability|debug|incident|runbook" CLAUDE.md
```

Verdict:

- **OK** if multiple narrow, well-described skills exist for recurring workflows, or commands exist and are intentionally kept.
- **KO** if no skills/commands exist and `CLAUDE.md` carries workflow content that should be skills.
- **OK with note** if the repo is small and has no recurring specialized workflows.

Remediation if KO:

- List workflow sections in `CLAUDE.md` that should become skills.
- Propose folder structure:

```text
.claude/
  skills/
    verify-change/
      SKILL.md
    review-pr/
      SKILL.md
    debug-incident/
      SKILL.md
```

Skill template:

```md
---
description: Use this when <specific trigger condition>.
allowed-tools: Bash, Read, Grep, Glob
---

# <Skill name>

## When to use
## Steps
## Verification
## Output format
```

---

