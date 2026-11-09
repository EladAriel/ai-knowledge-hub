# DEVX-013: v2.1.299 managed baseline

## Summary

(Claude Code) combines a version floor, read routing, MCP allow rules written for the new exact-match behavior, and deny rules.

## Details

Credit: release notes and the permissions docs. Managed settings with requiredMinimumVersion 2.1.299, env CLAUDE_CODE_DISABLE_FILE_MENTIONS=1, allow mcp__github__get_*, deny rules for risky Bash git.

## Content

- **[v2.1.299 managed baseline](https://github.com/anthropics/claude-code/releases/tag/v2.1.299)** (Claude Code) combines a version floor, read routing, MCP allow rules written for the new exact-match behavior, and the `--no-verify` block. Effort ~10 min. Credit: release notes and the [permissions docs](https://code.claude.com/docs/en/permissions).
```json
{ "requiredMinimumVersion": "2.1.299",
  "env": { "CLAUDE_CODE_DISABLE_FILE_MENTIONS": "1" },
  "permissions": { "allow": ["mcp__github__get_*"], "deny": ["Bash(git commit *--no-verify*)"] } }
```

## Sources

- [v2.1.299 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.299)
- [permissions docs](https://code.claude.com/docs/en/permissions)