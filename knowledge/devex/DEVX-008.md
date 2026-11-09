# DEVX-008: One git worktree per agent task (+ parallel-agent worktrees)

## Summary

Two MCP repos turned this into an AGENTS.md rule, because parallel agent sessions in one checkout collide.

## Details

Each task gets its own worktree and branch, so a 'git switch' in one session can't touch another's files.

## Sources

- [PR #5139](https://github.com/modelcontextprotocol/servers/pull/5139)
- [inspector PR #2663](https://github.com/modelcontextprotocol/inspector/pull/2663)
- [subagent docs](https://code.claude.com/docs/en/sub-agents)
- [Claude Code docs](https://code.claude.com/docs/en/settings-reference)
- [Cursor docs](https://cursor.com/docs)
