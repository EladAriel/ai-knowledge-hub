# DEVX-034: blockWritesOutsideWorkingDirectories (Claude Code 2.1.314)

## Summary

Refuses Write and Edit outside the working directories in every permission mode; doesn't cover Bash or MCP tools.

## Content

- **[blockWritesOutsideWorkingDirectories](https://github.com/anthropics/claude-code/releases/tag/v2.1.314)** (Claude Code 2.1.314) refuses Write and Edit outside the working directories in every permission mode. It doesn't cover Bash or MCP tools. Effort is about 5 min.
```json
{ "permissions": { "blockReadsOutsideWorkingDirectories": true, "blockWritesOutsideWorkingDirectories": true } }
```

## Sources

- [Claude Code v2.1.314](https://github.com/anthropics/claude-code/releases/tag/v2.1.314)
