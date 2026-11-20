# DEVX-096: Claude Code 2.1.328 alerts: auto mode default on more providers, PostToolUse audit gap, fail-closed MCP policy hook

## Summary

2.1.328: auto mode now starts by default on Bedrock, Google Agent Platform, Foundry and the Claude apps gateway (Opus/Sonnet 4.6, when no permission mode is set); pin a mode as in DEVX-090. Managed PostToolUse hooks no longer fire for calls that were refused before they ran, so an audit log that counts refusals there should also log PostToolBatch. New mod: an mcp_tool policy hook with onFailure block (2.1.328+).

## Details

- Auto mode default: if you want a fixed mode, set `defaultMode`/`disableAutoMode` in managed settings (same snippet as Nov 18, see DEVX-090).
- Audit gap: managed `PostToolUse` hooks no longer fire for calls refused before they ran. If your audit log counts refusals there, also log `PostToolBatch`.
- Mod, fail-closed MCP policy check (2.1.328+, ~5 min): if your MCP security-scan tool errors or is offline, the edit is blocked instead of slipping through. Docs still list `onFailure` for command/HTTP hooks only, so test it once.

```json
{"hooks":{"PreToolUse":[{"matcher":"Write|Edit","hooks":[{"type":"mcp_tool","server":"my_server","tool":"security_scan","input":{"file_path":"${tool_input.file_path}"},"onFailure":"block"}]}]}}
```

- Related: DEVX-088 (2.1.326/2.1.327 alerts), DEVX-090 (pin the starting permission mode). `onFailure: "block"` was already available for command and HTTP hooks.

## Content

Nov 19 alerts:

- **Claude Code 2.1.328: auto mode now starts by default on Bedrock, Google Agent Platform, Foundry and the Claude apps gateway** (Opus/Sonnet 4.6, when no permission mode is set). If you want a fixed mode, set `defaultMode`/`disableAutoMode` in managed settings (same snippet as Nov 18). [Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.328)
- **2.1.328 audit gap:** managed `PostToolUse` hooks no longer fire for calls that were refused before they ran. If your audit log counts refusals there, also log `PostToolBatch`. [Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.328)
- **Fail-closed MCP policy check (2.1.328+):** if your MCP security-scan tool errors or is offline, the edit is blocked instead of slipping through. ~5 min. Docs still list `onFailure` for command/HTTP hooks only, so test it once.

```json
{"hooks":{"PreToolUse":[{"matcher":"Write|Edit","hooks":[{"type":"mcp_tool","server":"my_server","tool":"security_scan","input":{"file_path":"${tool_input.file_path}"},"onFailure":"block"}]}]}}
```

## Sources

- [2.1.328 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.328)
