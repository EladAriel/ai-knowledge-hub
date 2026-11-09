# DEVX-035: CLAUDE_CODE_SUBAGENT_EFFORT (Claude Code 2.1.316)

## Summary

Runs subagents at a lower effort than the main session, cutting tokens on fan-out work; not in the docs yet.

## Details

{ "env": { "CLAUDE_CODE_SUBAGENT_EFFORT": "medium" } } (value is the agent's choice).

## Content

- **[CLAUDE_CODE_SUBAGENT_EFFORT](https://github.com/anthropics/claude-code/releases/tag/v2.1.316)** (Claude Code 2.1.316) runs subagents at a lower effort than the main session, which cuts token use on fan-out work. It isn't in the docs yet, and the value is my choice. Effort is about 5 min.
```json
{ "env": { "CLAUDE_CODE_SUBAGENT_EFFORT": "medium" } }
```

## Sources

- [Claude Code v2.1.316](https://github.com/anthropics/claude-code/releases/tag/v2.1.316)