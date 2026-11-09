# DEVX-010: Cursor agent-hygiene rule

## Summary

Gives each task its own worktree and paces bulk GitHub writes (~5 min). Adapted from the MCP maintainers' AGENTS.md. '.cursor/rules/agent-hygiene.mdc' (alwaysApply): start every task in a NEW git worktree; remove it when the PR merges or closes; pace bulk GitHub writes 1 s apart, never parallel, under 80/min and 500/hour.

## Details

Adapted from the MCP maintainers' AGENTS.md. '.cursor/rules/agent-hygiene.mdc' (alwaysApply): start every task in a NEW git worktree; remove it when the PR merges or closes; pace bulk GitHub writes 1 s apart, never parallel, under 80/min and 500/hour.

## Sources

- [MCP servers AGENTS.md](https://github.com/modelcontextprotocol/servers/blob/v2/main/AGENTS.md)
