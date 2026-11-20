# DEVX-023: Fleet-wide MCP and connector block

## Summary

Denies named MCP servers and claude.ai connectors from managed settings. Since Nov 19, the block also covers cloud and self-hosted runner sessions; prefer matching by `serverUrl` over the display name.

## Details

Effort: ~5 min (the Nov 19 connector-only variant takes ~3 min).

Base mod (Oct 21), credit: the Claude Code settings reference. In managed settings:

```json
{ "deniedMcpServers": [ { "serverName": "filesystem" }, { "serverName": "claude.ai Slack" } ],
  "disableClaudeAiConnectors": true }
```

Nov 19 update (managed-mcp docs): blocking a claude.ai connector everywhere now also applies to cloud sessions and self-hosted runner sessions. Prefer `serverUrl` over the display name when you match a server.

## Content

### Ready-to-use mods (Claude Code / Cursor)

- **Fleet-wide MCP and connector block** (~5 min): denies named MCP servers and claude.ai connectors from managed settings. Credit: [settings reference](https://code.claude.com/docs/en/settings-reference).

```json
{ "deniedMcpServers": [ { "serverName": "filesystem" }, { "serverName": "claude.ai Slack" } ],
  "disableClaudeAiConnectors": true }
```

- **Block a claude.ai connector everywhere** (~3 min, Nov 19): this now also covers cloud and self-hosted runner sessions. Prefer `serverUrl` over the display name. Credit: [managed-mcp docs](https://code.claude.com/docs/en/managed-mcp).

```json
{"deniedMcpServers":[{"serverName":"claude.ai Slack"}]}
```

## Sources

- [settings reference](https://code.claude.com/docs/en/settings-reference)
- [managed-mcp docs](https://code.claude.com/docs/en/managed-mcp)
