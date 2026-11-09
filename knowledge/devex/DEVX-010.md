# DEVX-010: Cursor agent-hygiene rule

## Summary

Gives each task its own worktree and paces bulk GitHub writes (~5 min).

## Content

**[Cursor agent-hygiene rule](https://github.com/modelcontextprotocol/servers/blob/v2/main/AGENTS.md)**, adapted S.md (~5 min). Put it in `.cursor/rules/agent-hygiene.mdc`:
```markdown
---
description: Isolation and pacing rules for agent sessions
alwaysApply: true
---
- Start every task in a NEW git worktree; never switch branches in the primary checkout:
  git worktree add --no-track ../<repo>-<task> -b <branch> origin/main
- Remove the worktree when the PR merges or is closed.
- Pace bulk GitHub writes: 1 s apart, never parallel, under 80/min and 500/hour.
```

No new Claude Code release today (still v2.1.296), and nothing new from Cursor or Aider.

## Sources

- [MCP servers AGENTS.md](https://github.com/modelcontextprotocol/servers/blob/v2/main/AGENTS.md)
