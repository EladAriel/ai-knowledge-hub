# DEVX-101: Cursor: make your MCP guard hook fail closed (beforeMCPExecution with failClosed)

## Summary

Cursor mod: if your MCP guard hook script crashes or times out, the MCP call is blocked instead of going through. ~3 min. It doesn't run in cloud agents.

## Details

- Add to `.cursor/hooks.json`:

```json
{"version":1,"hooks":{"beforeMCPExecution":[{"command":".cursor/hooks/mcp-guard.sh","failClosed":true}]}}
```

- Caveat: hooks do not run in cloud agents.
- Tip for unattended runs: include Cursor's `failClosed` in the same preflight that checks Claude Code security hooks for `"onFailure": "block"` (see DEVX-098).
- Effort: ~3 min. Reported Nov 22.
- Related: DEVX-096 (Claude Code fail-closed `mcp_tool` hook), DEVX-098 (`"onFailure": "block"` for Claude Code hooks).

## Content

### Cursor: make your MCP guard hook fail closed

If the guard script crashes or times out, the MCP call is blocked. ~3 min. It doesn't run in cloud agents. Add to `.cursor/hooks.json`:

```json
{"version":1,"hooks":{"beforeMCPExecution":[{"command":".cursor/hooks/mcp-guard.sh","failClosed":true}]}}
```

See [Cursor hooks](https://cursor.com/docs/hooks); the Claude Code counterpart is described in the [Code Mode docs](https://code.claude.com/docs/en/code-mode).

## Sources

- [Cursor hooks docs](https://cursor.com/docs/hooks)
- [Code Mode docs](https://code.claude.com/docs/en/code-mode)
