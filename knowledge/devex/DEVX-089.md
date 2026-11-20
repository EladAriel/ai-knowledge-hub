# DEVX-089: Keep MCP tokens out of your shell history with `claude mcp add-json -`

## Summary

Since 2.1.327, `claude mcp add-json \<name> -` reads the server's JSON from stdin. The token no longer sits in shell history or in `ps` output. Note that it still ends up in the saved config, and this does not work inside a Claude Code session. Enterprise feasibility: High. Stage: Adopt. Effort: about 2 minutes.

## Details

How it works: pipe the JSON in from your secret manager instead of pasting it as an argument. Practical PoC (needs 2.1.327+):
```bash
claude update
op read "op://Dev/acme-mcp/token" \
 | jq -R '{type:"http",url:"https://mcp.acme.example/mcp",headers:{Authorization:("Bearer "+.)}}' \
 | claude mcp add-json acme -
```
Success metric: `grep -E "add-json.*Bearer" ~/.bash_history ~/.zsh_history` returns nothing, and your onboarding docs use the stdin form. Seen in 5 sources. Expires Feb 16, 2027.

## Sources

- [2.1.327 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.327)
- [MCP docs: add from JSON](https://code.claude.com/docs/en/mcp#add-mcp-servers-from-json-configuration)
- [@alexmichael on X](https://x.com/alexmichael/status/2122832083298963706)
- [@Khaled865412521 on X](https://x.com/Khaled865412521/status/2122844172755353771)
- [@ClaudeCodeLog on X](https://x.com/ClaudeCodeLog/status/2122835481855394129)
