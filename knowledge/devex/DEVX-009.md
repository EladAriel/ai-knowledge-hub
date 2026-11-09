# DEVX-009: Read-only Haiku researcher subagent

## Summary

A cheap explorer subagent that can't edit anything (~5 min).

## Details

Credit: the Claude Code docs, pattern popularized by @davidarngar and @SteticIA on X. '.claude/agents/researcher.md' with tools: Read, Grep, Glob and model: haiku; never modify files, propose changes in the report.

## Content

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

## Sources

- [subagent docs](https://code.claude.com/docs/en/sub-agents)