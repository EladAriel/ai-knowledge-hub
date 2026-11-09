# DEVX-006: Subagent autoCompactWindow

## Summary

'autoCompactWindow' (Claude Code 2.1.296 or later) for subagents.

## Details

A long research subagent compacts its context earlier than the main session, which caps token burn. Put it in '.claude/agents/deep-research.md' frontmatter.

## Content

## Ready-to-use mods (Claude Code / Cursor)

**Subagent `autoCompactWindow` (Claude Code 2.1.296 or later).** A long research subagent compacts its context earlier than the main session, which caps token burn. **Effort:** ~5 min. Put this in `.claude/agents/deep-research.md`:
```markdown
---
name: deep-research
description: Long codebase research; keep findings short for the parent.
tools: Read, Grep, Glob
model: haiku
autoCompactWindow: 200000
---
Research only. Return a short summary with file paths; do not dump full file bodies to the parent.
```
Source: [Claude Code v2.1.296](https://github.com/anthropics/claude-code/releases/tag/v2.1.296)

## Sources

- [Claude Code v2.1.296](https://github.com/anthropics/claude-code/releases/tag/v2.1.296)