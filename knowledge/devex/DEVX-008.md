# DEVX-008: One git worktree per agent task (+ parallel-agent worktrees)

## Summary

Two MCP repos turned this into an AGENTS.md rule, because parallel agent sessions in one checkout collide.

## Details

Each task gets its own worktree and branch, so a 'git switch' in one session can't touch another's files. PoC: 'git worktree add --no-track ../\<repo>-\<N> -b \<branch> origin/main'. Follow-up (Oct 21): Claude Code 'worktree.baseRef' + '.worktreeinclude', Cursor '.cursor/worktrees.json'; keep the copied env list short.

## Content

## 5. One git worktree per agent task (Feasibility: High, Stage: Trial)
- **What changed:** two MCP repos turned this into an AGENTS.md rule this week, because parallel agent sessions in one checkout were leaking each other's edits and build output.
- **How it works:** each task gets its own worktree and branch, so a `git switch` in one session can't touch another's files.
- **Effort:** ~5 min.
- **PoC:** run `git worktree add --no-track ../<repo>-<N> -b <branch> origin/main`, or add `isolation: worktree` to the subagent frontmatter.
- **Success metric:** no leaked-change incidents when agents run in parallel.
- **Sources (3):** [PR #5139](https://github.com/modelcontextprotocol/servers/pull/5139), [inspector PR #2663](https://github.com/modelcontextprotocol/inspector/pull/2663), [subagent docs](https://code.claude.com/docs/en/sub-agents)

## Ready-to-use mods (Claude Code / Cursor)
- [Read-only Haiku researcher subagent](https://code.claude.com/docs/en/sub-agents) gives you a cheap explorer that can't edit anything (~5 min). Credit: the Claude Code docs, with the pattern popularized by @davidarngar and @SteticIA on X.
```
# .claude/agents/researcher.md
---
name: researcher
description: Read-only codebase research and impact analysis. Use proactively before edits.
tools: Read, Grep, Glob
model: haiku
---
Investigate and report findings with exact file paths and line numbers.
Never modify files; propose changes in your report instead.
```

## Ready-to-use mods (Claude Code / Cursor)
- **Parallel-agent worktrees** (~10 min) gives every parallel agent its own checkout with env files copied in. Keep the copied list short, because each worktree gets those secrets. Credit: [Claude Code docs](https://code.claude.com/docs/en/settings-reference) and [Cursor docs](https://cursor.com/docs).
```jsonc
// Claude Code settings.json, then: claude --worktree auth
{ "worktree": { "baseRef": "head" } }
// .worktreeinclude:  .env  .env.local
// Cursor .cursor/worktrees.json
{ "setup-worktree": ["npm ci", "cp $ROOT_WORKTREE_PATH/.env .env"] }
```

## Sources

- [PR #5139](https://github.com/modelcontextprotocol/servers/pull/5139)
- [inspector PR #2663](https://github.com/modelcontextprotocol/inspector/pull/2663)
- [subagent docs](https://code.claude.com/docs/en/sub-agents)
- [Claude Code docs](https://code.claude.com/docs/en/settings-reference)
- [Cursor docs](https://cursor.com/docs)