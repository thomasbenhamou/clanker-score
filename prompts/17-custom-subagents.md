# Pattern 17 — Custom Subagents Pattern

This is the detailed audit prompt for subagent 17. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 17 — Custom Subagents Pattern

Check whether project-specific subagents exist for recurring specialized work.

Investigation:

- Look for project agents:
  - `.claude/agents/*.md`
- For each agent:
  - read frontmatter
  - check description
  - check tool restrictions
  - check permissions
  - check whether it maps to repo needs
- Identify recurring specialized work from repo contents:
  - frontend review
  - backend review
  - security review
  - database migration review
  - architecture review
  - performance review
  - observability/debugging
  - API contract review
- Check whether generic agents are being used where a project-specific reviewer would be safer.

Useful commands:

```bash
find . -path "*/.claude/agents/*.md" -type f -not -path "*/node_modules/*" -not -path "*/.git/*"
find . -maxdepth 4 \( -name "migrations" -o -name "schema.sql" -o -name "openapi.yaml" -o -name "openapi.json" -o -name "swagger.yaml" -o -name "datadog" -o -name "monitors" -o -name "dashboards" \) -not -path "*/node_modules/*" -not -path "*/.git/*"
```

Verdict:

- **OK** if useful project-level subagents exist for recurring high-risk work.
- **KO** if the repo has repeated specialized work but only generic agents.
- **OK with note** if the repo is small or does not justify custom subagents.

Remediation if KO:

- Propose concrete agents based on repo contents.
- Include template:

```md
---
name: security-reviewer
description: Use this agent to review security-sensitive changes before PR/MR completion.
tools: Read, Grep, Glob, Bash
---

You are a read-only security reviewer for this repository.

Focus on:
- authentication
- authorization
- secrets
- input validation
- data exposure
- dependency risk

Return:
- findings
- affected files
- severity
- concrete remediation
```

---

