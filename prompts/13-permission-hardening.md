# Pattern 13 — Permission Hardening Pattern

This is the detailed audit prompt for subagent 13. Follow it exactly after reading `../GLOBAL.md`.

## Subagent 13 — Permission Hardening Pattern

Check whether dangerous operations and sensitive file edits are blocked through committed `permissions.deny`.

Investigation:

- Read `.claude/settings.json`.
- Read `.claude/settings.local.json` only for comparison; local-only rules do not count.
- Verify committed deny rules cover dangerous operations and sensitive files, at minimum:
  - force push
  - hard reset
  - recursive delete
  - `.env`
  - credentials
  - private keys
  - `.pem`
  - production deploy commands if relevant
  - destructive database commands if relevant
- Check whether existing rules are too broad, too narrow, or only local.

Useful commands:

```bash
test -f .claude/settings.json && cat .claude/settings.json
test -f .claude/settings.local.json && cat .claude/settings.local.json
```

Verdict:

- **OK** if `.claude/settings.json` has a `permissions.deny` block covering baseline dangerous operations and sensitive files.
- **KO** if no deny list exists, deny rules are only local, or major gaps exist.
- **OK with note** if the repo is read-only/docs-only and no destructive commands are relevant, but sensitive-file protection should still be considered.

Remediation if KO:

- Provide the exact missing deny rules.

Baseline snippet:

```json
{
  "permissions": {
    "deny": [
      "Bash(* push --force *)",
      "Bash(* push -f *)",
      "Bash(* reset --hard *)",
      "Bash(rm -rf *)",
      "Edit(*.env)",
      "Write(*.env)",
      "Edit(*.env.*)",
      "Write(*.env.*)",
      "Edit(*credentials*)",
      "Write(*credentials*)",
      "Edit(*.pem)",
      "Write(*.pem)",
      "Edit(*id_rsa*)",
      "Write(*id_rsa*)",
      "Edit(*id_ed25519*)",
      "Write(*id_ed25519*)"
    ]
  }
}
```

---

