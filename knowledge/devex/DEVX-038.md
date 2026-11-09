# DEVX-038: agentfence: one hook policy for Claude Code and Cursor

## Summary

Parses shell commands (chains, pipes, $(...), sudo/env wrappers); blocks rm -rf ~, force-push to main, curl | bash,.env reads, DROP TABLE; asks before terraform destroy and git reset --hard; JSONL audit log. Checks command text only, not a sandbox.

## Details

pipx install git+https://github.com/hamarshehmhmd/agentfence ; agentfence install claude --user ; agentfence install cursor --user. Per-repo .agentfence.toml: [settings] protected_branches = ["main", "release"]; [[custom]] id = "prod-db" pattern = "psql .*prod" action = "deny" reason = "Agents may not touch the production database". Caveats: one day old, one maintainer, AGPL-3.0 (check with legal).

## Sources

- [agentfence](https://github.com/hamarshehmhmd/agentfence)
