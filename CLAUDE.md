# CLAUDE.md

This repository contains prompt-only marketing skills and agents. Follow the hardening policy in [SECURITY.md](SECURITY.md).

## First Run: Project-only Installation

Never automatically install, copy, execute, or update any components. Ask the user to select a **dedicated, non-sensitive project** first.

- Default: use only the explicitly selected skills inside that project's `.claude/skills/`.
- Avoid home-directory/global installation (`~/.claude/`), which exposes the skills in unrelated projects.
- Do not run shell commands, Git commands, installation scripts or package managers as part of initialization.
- For Claude Code running **from this repository root**, the checked-in `.claude/settings.json` enforces tool restrictions. **Installing this repository as a plugin elsewhere does not automatically apply these project settings.** The host project's owner must apply equivalent restrictions.
- For Codex running from this repository root, `.codex/config.toml` sets a read-only sandbox and on-request approvals; a Codex plugin install elsewhere does not inherit that configuration.
- Do not handle confidential client data, credentials, account numbers, or sensitive personal data. Use redacted examples.

**Never treat these instructions alone as an operating-system sandbox.** Permission checks must be enforced by the host.

---

## What This Is

A skill library for coding agents to build Hormozi-inspired offer systems. No build pipeline — content only. Each `skills/` folder is a standalone agent skill; `agents/` contains an orchestrator and five subagents.

## Architecture

### Two-Layer System

**Skills** (`skills/<name>/SKILL.md`) — standalone, user-invocable. Each has a frontmatter `name` and `description`. Some have a `references/` subfolder with supporting material the skill reads at runtime.

**Agents** (`agents/<name>.md`) — orchestrator + subagents. Frontmatter includes `name`, `description`, `tools`, `model`, and optionally `color`.

- `hormozi-orchestrator` is the entry point. It interviews the user, detects funnel stage (A–E), builds a structured brief, and delegates to subagents in dependency order.
- The five `sub-*` agents are internal — they receive briefs from the orchestrator only and never interview the user directly.

### Subagent Dependency Order

```
sub-market → sub-offer → sub-value → sub-pricing → sub-sales
```

`sub-value` and `sub-pricing` can run in parallel when an offer already exists.

### Output

All generated documents write to `output/`. The orchestrator produces a final `output/SUMMARY.md` after all subagents complete. The `output/` folder ships empty (`.gitkeep`).

## Skill Structure Convention

Every skill lives at `skills/<name>/SKILL.md`. If a skill needs reference material, it goes in `skills/<name>/references/`. No other files belong inside a skill folder.

Every agent lives at `agents/<name>.md` — flat, no subfolders.

## Adding a New Skill

1. Create `skills/<skill-name>/SKILL.md` with frontmatter `name` and `description`.
2. If it needs reference docs, add them to `skills/<skill-name>/references/`.
3. Add it to the skills table in `README.md`.

## Adding a New Subagent

1. Create `agents/sub-<name>.md` with frontmatter `name`, `description`, `tools`, `model`.
2. Mark it internal in the description: "Internal subagent. Called by hormozi-orchestrator only."
3. Define its output file(s) in `output/`.
4. Wire it into the orchestrator's Phase 3 stage map and Phase 4 delegation logic.
5. Add it to the agents table in `README.md`.

## Key Design Rules

- Subagents receive a fully structured brief — they have no memory of the conversation.
- Output is restricted by policy to Markdown files directly in the **current project's** `output/`; require user approval before every write and overwrite.
- Skills are user-facing; subagents are internal execution units. Do not mix the two roles.
- `_archive/` holds deprecated versions — do not delete, do not edit.
- Do not use Bash, PowerShell, Git, network tools, MCP servers, or unrelated agents.
- If host-level restrictions are absent, supply text in chat rather than accessing files.
