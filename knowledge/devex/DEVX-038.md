# DEVX-038: agentfence: one hook policy for Claude Code and Cursor

## Summary

- agentfence is one hook policy for both Claude Code and Cursor. It parses shell commands, including chains, pipes, $(...) and sudo or env wrappers. It blocks rm -rf ~, force-pushes to main, curl | bash, reads of .env files and DROP TABLE.

## Details

pipx install git+https://github.com/hamarshehmhmd/agentfence ; agentfence install claude --user ; agentfence install cursor --user. Per-repo .agentfence.toml: [settings] protected_branches = ["main", "release"]; [[custom]] id = "prod-db" pattern = "psql .*prod" action = "deny" reason = "Agents may not touch the production database". Caveats: one day old, one maintainer, AGPL-3.0 (check with legal).

## Content

- **[agentfence](https://github.com/hamarshehmhmd/agentfence)** is one hook policy for both Claude Code and Cursor. It parses shell commands, including chains, pipes, `$(...)` and `sudo` or `env` wrappers. It blocks `rm -rf ~`, force-pushes to main, `curl | bash`, reads of `.env` files and `DROP TABLE`. It asks before `terraform destroy` and `git reset --hard`, and it keeps a JSONL audit log. It only checks command text, so it isn't a sandbox. The project is a day old with one maintainer, and its license is now AGPL-3.0, so check with legal first. Effort is about 15 min. The snippet is from its README:
```bash
pipx install git+https://github.com/hamarshehmhmd/agentfence
agentfence install claude --user
agentfence install cursor --user
```
```toml
# .agentfence.toml (per repo)
[settings]
protected_branches = ["main", "release"]
[[custom]]
id = "prod-db"
pattern = "psql .*prod"
action = "deny"
reason = "Agents may not touch the production database"
```

## Sources

- [agentfence](https://github.com/hamarshehmhmd/agentfence)