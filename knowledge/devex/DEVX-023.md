# DEVX-023: Fleet-wide MCP and connector block

## Summary

Denies named MCP servers and claude.ai connectors from managed settings.

## Details

Credit: settings reference. { 'deniedMcpServers': [ { 'serverName': 'filesystem' }, { 'serverName': 'claude.ai Slack' } ], 'disableClaudeAiConnectors': true }

## Content

## Ready-to-use mods (Claude Code / Cursor)
- **Fleet-wide MCP and connector block** (~5 min) denies named MCP servers and claude.ai connectors from managed settings. Credit: [settings reference](https://code.claude.com/docs/en/settings-reference).
```json
{ "deniedMcpServers": [ { "serverName": "filesystem" }, { "serverName": "claude.ai Slack" } ],
  "disableClaudeAiConnectors": true }
```

## Sources

- [settings reference](https://code.claude.com/docs/en/settings-reference)