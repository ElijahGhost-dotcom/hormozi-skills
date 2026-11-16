# Reviewed upstream baseline / manual update policy

- Upstream: https://github.com/alexsmedile/hormozi-skills
- Exact reviewed upstream commit: `910545c278d999cff14fd6d543f3df34ec0bbe4d`
- Fork at the start of hardening: same commit.
- This hardening intentionally **diverges from upstream**. It does not auto-sync.

## Updating

1. Inspect the upstream commit range and review **every added or changed file** (including Markdown instructions, plugin manifests, hooks, MCP configurations and workflows).
2. Reject new command execution, network exfiltration, unapproved writes, global installs or auto-updates.
3. Import selected changes manually on a fresh review branch; maintain a rollback commit and review the PR.
4. Do not auto-merge, auto-update, or replace the reviewed fork with upstream `main`.

This pin is documentation and a reproducible reference; GitHub itself does **not** prevent the owner from later merging another commit.
