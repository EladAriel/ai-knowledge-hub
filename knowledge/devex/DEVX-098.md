# DEVX-098: Claude Code 2.1.329/2.1.330 alerts: Code Mode hook crash no longer blocks, deniedMcpServers names narrowed; approve each Code Mode script

## Summary

2.1.330: a `deniedMcpServers` name entry now blocks only that one claude.ai connector, not others at the same address, so the `serverName` mod (DEVX-023) is weaker; deny the connector's exact URL instead (copy it from `/mcp`). 2.1.329 (Code Mode): a `PreToolUse` hook that crashes no longer blocks a script's tool call, so add `"onFailure": "block"` to every security hook; Code Mode can now also start with telemetry off, so keep the managed `CLAUDE_CODE_EXPERIMENTAL_CODE_MODE=0` if you need it off. Mod (~2 min): require approval for each Code Mode script.

## Details

- 2.1.330: deny the connector's exact URL instead of its name (copy it from `/mcp`).
- 2.1.329: add `"onFailure": "block"` to every security `PreToolUse` hook; keep managed `CLAUDE_CODE_EXPERIMENTAL_CODE_MODE=0` if you need Code Mode off.
- Mod, approve each Code Mode script before it runs (closes the gap left by the 2.1.329 hook change; press `Ctrl+O` to read the code; ~2 min). Add to `~/.claude/settings.json`:

```json
{"permissions":{"ask":["REPL"]}}
```

- Tip for unattended runs: add a preflight that walks every security hook in the Claude Code and Cursor settings and fails the run if a hook is missing `"onFailure": "block"` (`failClosed` in Cursor).
- Effort: ~2 min (mod). Reported Nov 22.
- Related: DEVX-023 (fleet-wide MCP/connector block), DEVX-087 (Code Mode trial), DEVX-096 (2.1.328 alerts), DEVX-101 (Cursor fail-closed MCP guard).

## Content

### Claude Code 2.1.330 changes how `deniedMcpServers` names work

A name entry now blocks only that one claude.ai connector, not other connectors at the same address, so the Nov 19 `serverName` mod is weaker than it was. Deny the connector's exact URL instead; you can copy the URL from `/mcp`. See the [2.1.330 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.330).

### Claude Code 2.1.329, Code Mode

A `PreToolUse` hook that crashes no longer blocks a Code Mode script's tool call. Add `"onFailure": "block"` to every security hook. Code Mode can now also start with telemetry off, so keep the managed `CLAUDE_CODE_EXPERIMENTAL_CODE_MODE=0` if you need Code Mode off. See the [2.1.329 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.329).

### Mod: approve each Code Mode script before it runs

This closes the gap left by the 2.1.329 hook change. Press `Ctrl+O` to read the code before approving. ~2 min. Add to `~/.claude/settings.json`:

```json
{"permissions":{"ask":["REPL"]}}
```

## Sources

- [2.1.330 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.330)
- [2.1.329 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.329)
- [Code Mode docs](https://code.claude.com/docs/en/code-mode)
