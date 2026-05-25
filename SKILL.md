---
description: Audit whether the current repository is optimized for maximum coding-agent efficiency: fast context retrieval, safe autonomy, deterministic verification, low-noise navigation, reproducible setup, and team-shareable Claude Code configuration. Dispatches one read-only subagent per pattern in parallel. The orchestrator stays lightweight: each subagent reads its own prompt file.
allowed-tools: Task, Bash, Read, Write, Glob, Grep
---

# Coding Agent Efficiency Audit

You are the orchestrator for a repository-level audit of Claude Code / coding-agent efficiency.

The goal is to evaluate whether a coding agent can quickly understand the repo, safely make changes, verify its own work, and operate with minimal wasted context or human hand-holding.

## Important efficiency rule

Do **not** read all detailed pattern prompts yourself.

Each subagent must read:
1. `~/.claude/skills/clanker-score/GLOBAL.md`
2. its own detailed prompt file under `~/.claude/skills/clanker-score/prompts/`

This keeps the orchestrator context small and lets each subagent load only what it needs.

## How to run

Dispatch **18 subagents IN PARALLEL** using the `Task` tool — one per pattern.

All 18 `Task` invocations MUST be sent in a single assistant message so they execute concurrently. Do not run them sequentially.

Use `Explore` as the subagent type if available. If `Explore` is unavailable, use `general-purpose`.

Every subagent must be explicitly told to be read-only.

## Pattern prompt files

1. Reproducible Development Environment Pattern — `~/.claude/skills/clanker-score/prompts/01-reproducible-development-environment.md`
2. Package Manager & Runtime Pinning Pattern — `~/.claude/skills/clanker-score/prompts/02-package-manager-runtime-pinning.md`
3. Repo Map Pattern — `~/.claude/skills/clanker-score/prompts/03-repo-map.md`
4. Context Cascade Pattern — `~/.claude/skills/clanker-score/prompts/04-context-cascade.md`
5. CLAUDE.md Quality Pattern — `~/.claude/skills/clanker-score/prompts/05-claude-md-quality.md`
6. Noise Filter Pattern — `~/.claude/skills/clanker-score/prompts/06-noise-filter.md`
7. Symbol Lookup Pattern — `~/.claude/skills/clanker-score/prompts/07-symbol-lookup.md`
8. Large-Repo File Discovery Pattern — `~/.claude/skills/clanker-score/prompts/08-large-repo-file-discovery.md`
9. Deterministic Checks Pattern — `~/.claude/skills/clanker-score/prompts/09-deterministic-checks.md`
10. Verifiable Work Loop Pattern — `~/.claude/skills/clanker-score/prompts/10-verifiable-work-loop.md`
11. CI Parity Pattern — `~/.claude/skills/clanker-score/prompts/11-ci-parity.md`
12. Fast Feedback / Focused Tests Pattern — `~/.claude/skills/clanker-score/prompts/12-fast-feedback-focused-tests.md`
13. Permission Hardening Pattern — `~/.claude/skills/clanker-score/prompts/13-permission-hardening.md`
14. Local Config Hygiene Pattern — `~/.claude/skills/clanker-score/prompts/14-local-config-hygiene.md`
15. Just-in-Time Skill Pattern — `~/.claude/skills/clanker-score/prompts/15-just-in-time-skill.md`
16. Agent Output / PR Hygiene Pattern — `~/.claude/skills/clanker-score/prompts/16-agent-output-pr-hygiene.md`
17. Custom Subagents Pattern — `~/.claude/skills/clanker-score/prompts/17-custom-subagents.md`
18. Harness Bundle Pattern — `~/.claude/skills/clanker-score/prompts/18-harness-bundle.md`

## Task dispatch payloads to create

Create one `Task` call per item below, all in the same assistant message:

```yaml
- description: "Reproducible Development Environment Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/01-reproducible-development-environment.md`. Then perform only Pattern 1: Reproducible Development Environment Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Package Manager & Runtime Pinning Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/02-package-manager-runtime-pinning.md`. Then perform only Pattern 2: Package Manager & Runtime Pinning Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Repo Map Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/03-repo-map.md`. Then perform only Pattern 3: Repo Map Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Context Cascade Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/04-context-cascade.md`. Then perform only Pattern 4: Context Cascade Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "CLAUDE.md Quality Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/05-claude-md-quality.md`. Then perform only Pattern 5: CLAUDE.md Quality Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Noise Filter Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/06-noise-filter.md`. Then perform only Pattern 6: Noise Filter Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Symbol Lookup Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/07-symbol-lookup.md`. Then perform only Pattern 7: Symbol Lookup Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Large-Repo File Discovery Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/08-large-repo-file-discovery.md`. Then perform only Pattern 8: Large-Repo File Discovery Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Deterministic Checks Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/09-deterministic-checks.md`. Then perform only Pattern 9: Deterministic Checks Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Verifiable Work Loop Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/10-verifiable-work-loop.md`. Then perform only Pattern 10: Verifiable Work Loop Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "CI Parity Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/11-ci-parity.md`. Then perform only Pattern 11: CI Parity Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Fast Feedback / Focused Tests Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/12-fast-feedback-focused-tests.md`. Then perform only Pattern 12: Fast Feedback / Focused Tests Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Permission Hardening Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/13-permission-hardening.md`. Then perform only Pattern 13: Permission Hardening Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Local Config Hygiene Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/14-local-config-hygiene.md`. Then perform only Pattern 14: Local Config Hygiene Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Just-in-Time Skill Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/15-just-in-time-skill.md`. Then perform only Pattern 15: Just-in-Time Skill Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Agent Output / PR Hygiene Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/16-agent-output-pr-hygiene.md`. Then perform only Pattern 16: Agent Output / PR Hygiene Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Custom Subagents Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/17-custom-subagents.md`. Then perform only Pattern 17: Custom Subagents Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
- description: "Harness Bundle Pattern"
  prompt: "Read `~/.claude/skills/clanker-score/GLOBAL.md` and `~/.claude/skills/clanker-score/prompts/18-harness-bundle.md`. Then perform only Pattern 18: Harness Bundle Pattern. You are read-only: do not edit, write, delete, move, or modify files. Return exactly the required subagent output format."
  subagent_type: "Explore if available, otherwise general-purpose"
```

## Final aggregated output

Once ALL 18 subagents return, produce a **single self-contained HTML file** as the consolidated report.

### How to deliver it

1. Capture the current timestamp by running `date "+%Y-%m-%d %H:%M %Z"` via the `Bash` tool and inject the result into the HTML header.
2. Write the HTML to a file at the repository root named `agent-efficiency-audit.html` using the `Write` tool. Overwrite if it already exists.
3. After writing, print the absolute file path to the user on a single line so they can open it. Do not print the HTML inline. Do not add any other commentary, preamble, or summary.

### HTML requirements

- Output must be a complete `<!DOCTYPE html>` document, self-contained (all CSS inline in a `<style>` block, no external assets). One small inline `<script>` is permitted **only** to power the CTA card's copy-to-clipboard button — no other scripts.
- Clear, light background. Dark, high-contrast text. Generous spacing, separators, and light pastel accents inside cards for readability.
- **Header** at the top: an `<h1>` title plus a timestamp line showing when the audit was generated (use the value captured via the `date` command).
- **Total Score banner** immediately after the header: one very large prominent number `XX`, a `/ 100` label, and a colored band based on the score. The number must be visually dominant (large, bold, tabular-nums).
- **CTA card** immediately after the Total Score banner, before any `<h2>` section heading. The card must be highly visible (vibrant accent background, white text, soft shadow). It contains the message `Ask your clanker to improve your set up` as the headline, one short supporting sentence, and a prominent **Click to copy prompt** button. Clicking the button copies the generated remediation prompt (see **Remediation prompt** section below) to the clipboard. Render the card even when there are no `KO` patterns — in that case the prompt simply says everything passed and there is nothing to do.
- Split the per-pattern detail into the four section groups below using `<h2>` headings.
- One **foldable card** per pattern using a `<details>` element. Cards are collapsed by default.
- Each card's `<summary>` must show: pattern number, pattern name, the pattern weight (e.g. `weight 10`), and a colored verdict pill (`OK` green, `KO` red, `OK with note` amber).
- Expanding the card must reveal, in this exact order, four visually-separated info blocks (each with a light pastel background and a colored left border):
  1. **Why does it matter?** — fixed per-pattern blurb. Use the text from the **Per-pattern fixed content** section below verbatim. Always shown.
  2. **What good looks like** — fixed per-pattern blurb. Use the text from the **Per-pattern fixed content** section below verbatim. Always shown.
  3. **What's currently in your repo** — the bullet list of evidence the subagent returned. Always shown.
  4. **What to do to make clanker happy** — only when verdict is `KO`; bullet list of concrete remediation actions (file paths, config snippets, commands).
- Apart from the Total Score banner, do **not** add a Summary section, counters, top-N priorities, quick wins, or strong-points list. The score banner + cards are the entire report.

### Total Score calculation

Each pattern has a fixed weight (sum = 100). Convert the subagent verdict to a percentage, then compute the weighted average.

**Verdict → percentage**

| Verdict | Percentage |
|---|---|
| `OK` | 100% |
| `OK with note` | 70% |
| `KO` | 0% |

**Pattern weights**

| # | Pattern | Weight |
|---:|---|---:|
| 1 | Reproducible Development Environment | 6 |
| 2 | Package Manager & Runtime Pinning | 4 |
| 3 | Repo Map | 5 |
| 4 | Context Cascade | 4 |
| 5 | CLAUDE.md Quality | 10 |
| 6 | Noise Filter | 6 |
| 7 | Symbol Lookup | 8 |
| 8 | Large-Repo File Discovery | 5 |
| 9 | Deterministic Checks | 10 |
| 10 | Verifiable Work Loop | 9 |
| 11 | CI Parity | 4 |
| 12 | Fast Feedback / Focused Tests | 6 |
| 13 | Permission Hardening | 6 |
| 14 | Local Config Hygiene | 3 |
| 15 | Just-in-Time Skill | 3 |
| 16 | Agent Output / PR Hygiene | 3 |
| 17 | Custom Subagents | 4 |
| 18 | Harness Bundle | 4 |

**Formula**

```
total_score = Σ (weight_i × verdict_pct_i) / 100
```

Round to the nearest integer for display. Always shown as `XX / 100`.

**Score band (color of the banner)**

- `>= 80` → green band (background `#ecfdf5`, text `#14532d`, number `#15803d`)
- `60–79` → amber band (background `#fffbeb`, text `#78350f`, number `#b45309`)
- `< 60`  → red band (background `#fef2f2`, text `#7f1d1d`, number `#b91c1c`)

### Verdict pill styling

- `OK` → light green background (`#dcfce7`), dark green text (`#14532d`).
- `KO` → light red background (`#fee2e2`), dark red text (`#7f1d1d`).
- `OK with note` → light amber background (`#fef3c7`), dark amber text (`#78350f`).

### Per-pattern fixed content

Inject the following blurbs into every card verbatim, in the order shown (Why first, then What good looks like). Do not paraphrase, shorten, or rewrite them.

**Pattern 1 — Reproducible Development Environment**
- Why does it matter? Without a clean-checkout install path, agents waste cycles guessing at undocumented local setup and hit "works on my machine" failures. An agent cannot start coding if it cannot get the app running, so every minute spent decoding tribal setup knowledge is a minute not spent shipping.
- What good looks like: A fresh clone can be installed, run, tested, and built using documented commands tied to real files (devcontainer, Dockerfile, Makefile, justfile, or a README/CLAUDE.md setup section). Prerequisites, services, env vars, and bootstrap steps are explicitly listed and match what the codebase actually uses.

**Pattern 2 — Package Manager & Runtime Pinning**
- Why does it matter? When the package manager or runtime version is ambiguous, agents may run `npm` in a `pnpm` project, use the wrong Node/Python version, or generate a second lockfile that conflicts with CI. These mismatches break builds, corrupt dependency state, and silently diverge local behavior from production.
- What good looks like: One package manager per ecosystem with a single lockfile, runtime versions pinned via `.nvmrc` / `.tool-versions` / `pyproject.toml` / etc., and Node projects declare a `packageManager` field. CLAUDE.md or README states the exact install/build/test commands so the agent never has to guess.

**Pattern 3 — Repo Map**
- Why does it matter? Without a top-level map, agents waste tokens grepping the whole tree to figure out where features live, especially in monorepos. A 30-line map saves hundreds of exploratory tool calls and prevents agents from editing the wrong service or duplicating logic.
- What good looks like: A `REPO_MAP.md` (or labeled section in README/CLAUDE.md) lists every top-level folder with a one-line purpose, ideally with owner and main entry point. Coverage matches the actual `ls` output and stays current as the structure evolves.

**Pattern 4 — Context Cascade**
- Why does it matter? A single bloated CLAUDE.md at the root forces agents to load thousands of lines of mostly-irrelevant guidance on every task, burning context and burying the rules that actually matter. Local conventions are also harder to keep current when they all live in one global file.
- What good looks like: The root CLAUDE.md stays focused on global rules (under ~200 lines), and subtree CLAUDE.md files carry local commands, domain terms, and gotchas where they apply. Each file has a clear scope and avoids repeating what the others say.

**Pattern 5 — CLAUDE.md Quality**
- Why does it matter? A CLAUDE.md full of generic platitudes ("write clean code"), stale instructions, or info the agent could infer from the code costs context without adding value, and sometimes actively misleads. The file is only useful when it captures what cannot be derived from reading files.
- What good looks like: CLAUDE.md is concise, repo-specific, and aligned with actual scripts and CI. It includes the non-obvious — exact commands, architectural decisions, env quirks, gotchas, branch/PR conventions — and skips standard language conventions, file-by-file tours, and duplicated README content.

**Pattern 6 — Noise Filter**
- Why does it matter? When `node_modules`, `dist`, `vendor`, `coverage`, and generated SDK folders are searchable, every grep returns hundreds of irrelevant hits and Reads consume context with minified or generated code. Real signal gets buried under build artifacts.
- What good looks like: A committed `.claude/settings.json` uses `permissions.deny` to block reads of noisy/generated paths that actually exist in the repo. Local-only exclusions do not count; the team setup needs to be checked in so every agent benefits.

**Pattern 7 — Symbol Lookup**
- Why does it matter? Without an LSP-backed code intelligence tool, agents fall back to grep for "find definition" or "find references", which is slow, noisy, and easily fooled by name collisions in large or strongly typed codebases. Real symbol lookup turns a multi-step search into a single deterministic call.
- What good looks like: An MCP server with LSP support (e.g. `serena`) or the official language plugin is configured for the dominant language(s) and visible in `.mcp.json` or `.claude/settings.json`. Coverage spans the languages that actually exist in the repo, not just the smallest one.

**Pattern 8 — Large-Repo File Discovery**
- Why does it matter? In a monorepo with thousands of files, blind grep and find produce slow, noisy results and exhaust context before the agent finds the right file. Without a discovery aid, agents can spend an entire session just locating where to make a change.
- What good looks like: A large repo provides at least one of: `REPO_MAP.md`, a workspace manifest (pnpm-workspace, nx, turbo, lerna), a fileSuggestion config, or a documented "how to find files" section in CLAUDE.md. Small repos can skip this without penalty.

**Pattern 9 — Deterministic Checks**
- Why does it matter? When quality enforcement is "remember to run the linter" in prose, agents (and humans) forget, run the wrong command, or skip checks under time pressure. Hooks make checks unavoidable and reproducible, so broken code never leaves the editor.
- What good looks like: `.claude/settings.json` wires `PostToolUse` hooks on Edit/Write/MultiEdit to real project commands (lint, typecheck, test) that actually exist in `package.json`/`Makefile`/etc. The hook commands are verified to resolve, not invented.

**Pattern 10 — Verifiable Work Loop**
- Why does it matter? An agent that cannot verify its own work has to hand back to a human just to know whether the change compiles or the tests pass. Without exact verification commands, the agent either guesses or stops short, slowing every task and increasing the chance of broken PRs.
- What good looks like: CLAUDE.md (or README/Makefile/justfile) has an explicit "Verification" or "Before submitting" section listing the exact install, lint, typecheck, test, focused-test, and build commands. The commands match real scripts and cover the checks that matter before a PR opens.

**Pattern 11 — CI Parity**
- Why does it matter? When local agent checks are weaker than CI, work passes locally and fails in the pipeline, forcing rework and slowing the feedback loop. Every CI-only check is a trap the agent walks into blind.
- What good looks like: Every meaningful CI check (lint, format, typecheck, test, build, security scan) has a documented local equivalent in CLAUDE.md/README, ideally wrapped in a single `make verify` or `just verify` command. The commands match the CI config and stay in sync as CI evolves.

**Pattern 12 — Fast Feedback / Focused Tests**
- Why does it matter? If the only documented way to test is "run the full suite", agents either wait minutes per iteration or skip testing entirely. Tight loops require running just the one file or package the agent is working on.
- What good looks like: CLAUDE.md documents how to run a single test file, a package/module scope, and the full suite, with concrete examples (`pytest path/file`, `vitest run path`, `go test ./pkg/foo`). Scripts like `test:unit`, `test:watch`, or `test:focused` exist when the framework supports them.

**Pattern 13 — Permission Hardening**
- Why does it matter? Without committed deny rules, a coding agent can force-push, hard-reset, `rm -rf`, or edit `.env` and key files. One bad call can leak secrets, corrupt git history, or wipe local work — and "I trust this one to be careful" does not scale.
- What good looks like: A committed `.claude/settings.json` has a `permissions.deny` block covering destructive bash (force push, hard reset, `rm -rf`) and sensitive files (`.env`, `.pem`, credentials, private keys). Rules live in team settings, not just `.local.json`, so every contributor benefits.

**Pattern 14 — Local Config Hygiene**
- Why does it matter? When `CLAUDE.local.md`, `settings.local.json`, `.env` files, or private keys are not gitignored, personal config and secrets can be committed by accident. The blast radius ranges from noisy diffs to leaked credentials in remote history.
- What good looks like: `.gitignore` excludes Claude-local files (`CLAUDE.local.md`, `.claude/settings.local.json`), `.env` variants (with `.env.example` whitelisted), and key/credential patterns. No matching files are currently tracked in git.

**Pattern 15 — Just-in-Time Skill**
- Why does it matter? Stuffing every workflow (security review, deploy, migration, release) into CLAUDE.md means agents load it all every session, wasting context on workflows they will not use. Skills load on demand, so specialized procedures stay available without taxing every task.
- What good looks like: `.claude/skills/` contains narrow, well-described skills (each with a `SKILL.md` and a clear "when to use" description) for recurring specialized workflows. CLAUDE.md stays lean and points to skills instead of inlining their content; legacy `.claude/commands/` are acceptable but skills are preferred for new work.

**Pattern 16 — Agent Output / PR Hygiene**
- Why does it matter? Without explicit PR/MR expectations, agents improvise summaries that omit tests run, risks, rollback notes, or screenshots — leaving reviewers to dig. Inconsistent output also makes Claude-authored changes harder to triage at scale.
- What good looks like: A PR/MR template (`.github/PULL_REQUEST_TEMPLATE.md` or `.gitlab/merge_request_templates/`) or a CLAUDE.md section tells agents to include summary, verification commands, risks, rollback notes, and UI screenshots. Attribution policy (whether to credit Claude in commits) is stated intentionally.

**Pattern 17 — Custom Subagents**
- Why does it matter? Generic subagents handle generic work, but recurring high-risk reviews (security, migrations, API contracts, performance) benefit from a focused agent with the right tools and scope baked in. Without them, sensitive work gets the same loose handling as routine changes.
- What good looks like: `.claude/agents/` contains project-specific subagents matched to the repo's actual risk surface (e.g. `security-reviewer` for an auth-heavy service, `migration-reviewer` for a repo with schema migrations). Each has a clear description, tool allowlist, and read-only scope where appropriate.

**Pattern 18 — Harness Bundle**
- Why does it matter? When skills, hooks, MCP config, and agents live only in one repo's `.claude/` folder, every other repo has to reinvent them, and improvements do not propagate. A reusable plugin/bundle lets a team apply the same setup to dozens of repos and keep it current centrally.
- What good looks like: The harness is packaged as a plugin (`plugin.json` / `.claude-plugin/` or referenced via `enabledPlugins`) or pulled from a shared internal marketplace. Skills, agents, and hooks are versioned together and consumed by multiple repos, not duplicated per project.

### Remediation prompt (copied by the CTA button)

Build a single plain-text prompt string and embed it inside a hidden `<textarea id="clanker-prompt">` placed right after the CTA card. The button's inline script reads `.value` from that textarea and writes it to the clipboard, so any characters that would break the textarea (`&` → `&amp;`, `<` → `&lt;`, and the literal sequence `</textarea>` if it ever appears) must be HTML-escaped — nothing else needs escaping.

The prompt is **organized by section group**, not by pattern, because the receiving agent must dispatch exactly one subagent per section (not one per pattern). Only include sections that contain at least one `KO` pattern; skip sections where every pattern is `OK` or `OK with note`. If no pattern is `KO` at all, emit a short prompt that says the repo passed and there is nothing to fix.

Use this template verbatim, replacing the bracketed slots. Keep the leading instructions intact so the receiving agent knows exactly how to dispatch:

```
You are a coding agent tasked with improving this repository's coding-agent efficiency setup, based on a /clanker-score audit (score: <SCORE>/100, generated <TIMESTAMP>).

The audit found the gaps listed below, grouped by section. Dispatch ONE subagent per section IN PARALLEL using the Task tool with subagent_type "general-purpose". All Task calls MUST be sent in a single assistant message so they run concurrently — do not dispatch sequentially, and do not split a section across multiple subagents.

Each subagent must:
- Implement every fix listed under its section (across all patterns in that section).
- Write/edit files directly; do not return content for the orchestrator to paste.
- Prefer extending existing files (CLAUDE.md, .claude/settings.json, .gitignore, PR templates, …) over creating duplicates.
- Verify each file path before writing. Do not introduce unrelated changes or delete unrelated files.
- Be read-aware: re-check the current state of the file before editing in case it has changed since the audit.

When all subagents return, summarize what changed (file-by-file) and recommend running /clanker-score again to confirm the improvements.

---

## Section 1 — Agent Efficiency Foundations

### Pattern <N> — <pattern name>
- <fix bullet 1, verbatim from the card's "What to do to make clanker happy" list>
- <fix bullet 2>

### Pattern <M> — <pattern name>
- <fix bullet>

## Section 2 — Context & Tooling
… (only include section blocks that contain at least one KO pattern; only include KO patterns within each section) …
```

Section group names and their pattern ranges (use these exact section titles in the prompt):

- **Agent Efficiency Foundations** → patterns 1–5
- **Context & Tooling** → patterns 6–8
- **Verification & Safety** → patterns 9–14
- **Reusable Agent Workflows** → patterns 15–17
- **Team Rollout & Continuous Improvement** → pattern 18

If there are zero `KO` patterns, replace the section blocks with a single line: `All 18 patterns passed — no remediation needed. You can close this prompt.`

### Required structure

Use this skeleton verbatim, replacing `<REPO_NAME>`, `<TIMESTAMP>`, `<SCORE>`, the score-band class, and the per-pattern verdict/evidence/remediation data. Keep the exact section group titles and pattern order from the dispatch list above. For every card, paste the matching "Why does it matter?" and "What good looks like" blurb from the section above — those two blocks are fixed text, not subagent output.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Coding Agent Efficiency Audit — <REPO_NAME></title>
<style>
  :root {
    --bg: #fafafa;
    --card-bg: #ffffff;
    --text: #1a1a1a;
    --text-muted: #6b7280;
    --border: #e5e7eb;
    --why-bg: #eff6ff;
    --why-accent: #3b82f6;
    --why-text: #1e3a8a;
    --good-bg: #f0fdf4;
    --good-accent: #22c55e;
    --good-text: #14532d;
    --current-bg: #f9fafb;
    --current-accent: #9ca3af;
    --current-text: #374151;
    --fix-bg: #fff7ed;
    --fix-accent: #f59e0b;
    --fix-text: #78350f;
  }
  * { box-sizing: border-box; }
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    background: var(--bg);
    color: var(--text);
    max-width: 1000px;
    margin: 0 auto;
    padding: 2.5rem 1.5rem 4rem;
    line-height: 1.6;
  }
  header h1 {
    font-size: 2.1rem;
    margin: 0 0 0.35rem;
    font-weight: 800;
    letter-spacing: -0.02em;
  }
  header .timestamp {
    color: var(--text-muted);
    font-size: 0.9rem;
    font-variant-numeric: tabular-nums;
    margin-bottom: 1.75rem;
  }
  h2 {
    font-size: 0.85rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--text-muted);
    margin: 2.75rem 0 0.85rem;
    font-weight: 700;
  }
  .score {
    margin: 0 0 2.5rem;
    padding: 1.75rem 2rem;
    border-radius: 14px;
    display: flex;
    align-items: center;
    gap: 1.75rem;
    border: 1px solid rgba(0,0,0,0.05);
    box-shadow: 0 1px 3px rgba(0,0,0,0.04);
  }
  .score-value {
    font-family: "SF Pro Display", -apple-system, "Segoe UI", system-ui, sans-serif;
    font-size: 5rem;
    font-weight: 800;
    line-height: 1;
    letter-spacing: -0.045em;
    font-variant-numeric: tabular-nums;
  }
  .score-meta { display: flex; flex-direction: column; gap: 0.3rem; }
  .score-label { font-size: 1.05rem; font-weight: 700; letter-spacing: -0.01em; }
  .score-sub { font-size: 0.82rem; opacity: 0.75; }
  .score.green { background: #ecfdf5; color: #14532d; }
  .score.green .score-value { color: #15803d; }
  .score.amber { background: #fffbeb; color: #78350f; }
  .score.amber .score-value { color: #b45309; }
  .score.red   { background: #fef2f2; color: #7f1d1d; }
  .score.red   .score-value { color: #b91c1c; }

  .cta {
    margin: 0 0 2.5rem;
    padding: 1.5rem 1.75rem;
    border-radius: 14px;
    background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%);
    color: #ffffff;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1.5rem;
    box-shadow: 0 6px 20px rgba(79, 70, 229, 0.28);
  }
  .cta-text { flex: 1; min-width: 0; }
  .cta-text h3 {
    margin: 0 0 0.35rem;
    font-size: 1.2rem;
    font-weight: 800;
    letter-spacing: -0.01em;
  }
  .cta-text p {
    margin: 0;
    font-size: 0.9rem;
    opacity: 0.92;
    line-height: 1.5;
  }
  .cta-button {
    flex-shrink: 0;
    background: #ffffff;
    color: #4f46e5;
    border: none;
    padding: 0.8rem 1.35rem;
    border-radius: 8px;
    font-size: 0.92rem;
    font-weight: 700;
    cursor: pointer;
    letter-spacing: -0.005em;
    transition: transform 0.1s ease, background 0.15s ease, color 0.15s ease;
    font-family: inherit;
    box-shadow: 0 2px 6px rgba(0,0,0,0.12);
  }
  .cta-button:hover { background: #f5f3ff; transform: translateY(-1px); }
  .cta-button:active { transform: translateY(0); }
  .cta-button.copied { background: #dcfce7; color: #14532d; }
  @media (max-width: 600px) {
    .cta { flex-direction: column; align-items: flex-start; }
    .cta-button { width: 100%; }
  }
  #clanker-prompt { position: absolute; left: -9999px; top: -9999px; width: 1px; height: 1px; opacity: 0; }

  details {
    border: 1px solid var(--border);
    border-radius: 10px;
    margin: 0.7rem 0;
    background: var(--card-bg);
    overflow: hidden;
    transition: box-shadow 0.15s ease;
  }
  details[open] { box-shadow: 0 2px 10px rgba(0,0,0,0.05); }
  summary {
    cursor: pointer;
    font-weight: 600;
    list-style: none;
    display: flex;
    align-items: center;
    gap: 0.55rem;
    padding: 0.95rem 1.1rem;
    user-select: none;
  }
  summary:hover { background: #fafbfc; }
  summary::-webkit-details-marker { display: none; }
  summary::before {
    content: "▸";
    color: #9ca3af;
    transition: transform 0.15s ease;
    font-size: 0.85em;
  }
  details[open] > summary::before { transform: rotate(90deg); }
  .pattern-num { color: var(--text-muted); font-weight: 500; margin-right: 0.1rem; }
  .weight {
    display: inline-block;
    padding: 0.12rem 0.55rem;
    margin-left: 0.4rem;
    border-radius: 4px;
    background: #f3f4f6;
    color: #4b5563;
    font-size: 0.7rem;
    font-weight: 600;
    letter-spacing: 0.04em;
  }
  .pill {
    display: inline-block;
    padding: 0.2rem 0.7rem;
    border-radius: 999px;
    font-size: 0.7rem;
    font-weight: 700;
    margin-left: auto;
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }
  .ok   { background: #dcfce7; color: #14532d; }
  .ko   { background: #fee2e2; color: #7f1d1d; }
  .note { background: #fef3c7; color: #78350f; }

  .body {
    padding: 0.25rem 1.1rem 1.15rem;
    border-top: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }
  .info-block {
    margin: 0;
    padding: 0.9rem 1.05rem;
    border-radius: 8px;
    border-left: 3px solid;
  }
  .info-block:first-child { margin-top: 1rem; }
  .info-block h4 {
    margin: 0 0 0.45rem;
    font-size: 0.72rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    font-weight: 700;
  }
  .info-block p,
  .info-block ul { margin: 0; font-size: 0.93rem; }
  .info-block ul { padding-left: 1.25rem; }
  .info-block li { margin: 0.22rem 0; }

  .why     { background: var(--why-bg);     border-left-color: var(--why-accent);     color: var(--why-text); }
  .why h4     { color: var(--why-accent); }
  .good    { background: var(--good-bg);    border-left-color: var(--good-accent);    color: var(--good-text); }
  .good h4    { color: var(--good-accent); }
  .current { background: var(--current-bg); border-left-color: var(--current-accent); color: var(--current-text); }
  .current h4 { color: var(--current-accent); }
  .fix     { background: var(--fix-bg);     border-left-color: var(--fix-accent);     color: var(--fix-text); }
  .fix h4     { color: var(--fix-accent); }

  code { background: rgba(0,0,0,0.07); padding: 0.08rem 0.34rem; border-radius: 3px; font-size: 0.88em; font-family: "SF Mono", Menlo, Consolas, monospace; }
  pre  { background: #f3f4f6; border: 1px solid var(--border); border-radius: 6px; padding: 0.7rem; overflow-x: auto; font-size: 0.85rem; }
</style>
</head>
<body>
<header>
  <h1>Coding Agent Efficiency Audit — <REPO_NAME></h1>
  <div class="timestamp">Generated <TIMESTAMP></div>
</header>

<!-- Replace class with green / amber / red based on score band. -->
<div class="score green">
  <div class="score-value"><SCORE></div>
  <div class="score-meta">
    <div class="score-label">out of 100 &middot; Coding Agent Efficiency</div>
    <div class="score-sub">weighted across 18 patterns &middot; OK = 100% &middot; OK with note = 70% &middot; KO = 0%</div>
  </div>
</div>

<div class="cta">
  <div class="cta-text">
    <h3>Ask your clanker to improve your set up</h3>
    <p>Copy a ready-to-use prompt that dispatches one subagent per section to implement every proposed fix in parallel.</p>
  </div>
  <button type="button" class="cta-button" id="copy-prompt-btn">Click to copy prompt</button>
</div>
<textarea id="clanker-prompt" readonly aria-hidden="true" tabindex="-1"><!-- INSERT GENERATED REMEDIATION PROMPT HERE, HTML-ESCAPED (& → &amp;amp;, < → &amp;lt;) --></textarea>
<script>
(function () {
  var btn = document.getElementById('copy-prompt-btn');
  var src = document.getElementById('clanker-prompt');
  if (!btn || !src) return;
  var originalLabel = btn.textContent;
  function flashCopied() {
    btn.textContent = 'Copied!';
    btn.classList.add('copied');
    setTimeout(function () {
      btn.textContent = originalLabel;
      btn.classList.remove('copied');
    }, 2000);
  }
  function fallbackCopy() {
    src.style.left = '0'; src.style.top = '0'; src.style.opacity = '0';
    src.select();
    try { document.execCommand('copy'); } catch (e) {}
    src.style.left = '-9999px'; src.style.top = '-9999px';
  }
  btn.addEventListener('click', function () {
    var text = src.value;
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(text).then(flashCopied, function () { fallbackCopy(); flashCopied(); });
    } else {
      fallbackCopy();
      flashCopied();
    }
  });
})();
</script>

<h2>Agent Efficiency Foundations</h2>
<!-- One <details> card per pattern, 1 through 5. Example structure below; repeat for each card. -->
<details>
  <summary><span class="pattern-num">1.</span> Reproducible Development Environment Pattern <span class="weight">weight 6</span> <span class="pill ko">KO</span></summary>
  <div class="body">
    <div class="info-block why">
      <h4>Why does it matter?</h4>
      <p><!-- paste Pattern 1 "Why does it matter?" blurb verbatim --></p>
    </div>
    <div class="info-block good">
      <h4>What good looks like</h4>
      <p><!-- paste Pattern 1 "What good looks like" blurb verbatim --></p>
    </div>
    <div class="info-block current">
      <h4>What's currently in your repo</h4>
      <ul>
        <li><!-- evidence bullet from subagent --></li>
      </ul>
    </div>
    <!-- Only render the block below when verdict is KO. Omit entirely for OK or OK with note. -->
    <div class="info-block fix">
      <h4>What to do to make clanker happy</h4>
      <ul>
        <li><!-- concrete remediation action with file paths / commands --></li>
      </ul>
    </div>
  </div>
</details>
<!-- ... cards 2–5 ... -->

<h2>Context & Tooling</h2>
<!-- Cards 6, 7, 8 -->

<h2>Verification & Safety</h2>
<!-- Cards 9, 10, 11, 12, 13, 14 -->

<h2>Reusable Agent Workflows</h2>
<!-- Cards 15, 16, 17 -->

<h2>Team Rollout & Continuous Improvement</h2>
<!-- Card 18 -->

</body>
</html>
```

## Rules

- Dispatch all 18 `Task` calls in one assistant message. Sequential dispatch fails the audit.
- Do not read all pattern prompt files in the orchestrator.
- Subagents must inspect actual files. No verdict from assumptions.
- Subagents must be read-only.
- Keep remediation concrete: file paths, config snippets, and commands.
- For patterns that genuinely do not apply, use **OK with note** and briefly explain.
- Do not punish small repos for skipping high-cost setup.
- Do not reward stale or copied config.
- Do not count local-only config as team setup.
- The "Why does it matter?" and "What good looks like" blocks are fixed text from the **Per-pattern fixed content** section — paste them verbatim, do not rewrite per run.
- The final deliverable is the HTML file only. Do not print a Markdown summary or top-N list to stdout — the only top-level summary is the Total Score banner inside the HTML; every other detail belongs inside the per-pattern foldable cards.
