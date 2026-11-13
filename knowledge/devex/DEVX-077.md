# DEVX-077: Cap nested subagents at 2 levels (CLAUDE_CODE_MAX_SUBAGENT_SPAWN_DEPTH)

## Summary

Ready-to-use Claude Code mod: limit nested subagents to 2 levels (default 3) so delegation trees can't run up token costs. ~1 min.

## Details

In `.claude/settings.json`: `{ "env": { "CLAUDE_CODE_MAX_SUBAGENT_SPAWN_DEPTH": "2" } }`. Setting is from Anthropic's sub-agents docs. A related practice: set both CLAUDE_CODE_MAX_SUBAGENT_SPAWN_DEPTH (default 3 layers; 1 turns nesting off) and CLAUDE_CODE_MAX_CONCURRENT_SUBAGENTS (default 20) as environment variables from a launcher or pre-launch script, without touching the repo settings.json. The tool enforces the limits, so they do not depend on the model complying. Effort ~10 min.

## Content

- [Subagent depth cap (Claude Code)](https://code.claude.com/docs/en/sub-agents): limits nested subagents to 2 levels (the default is 3) so delegation trees can't run up token costs. ~1 min. In `.claude/settings.json`:
```json
{ "env": { "CLAUDE_CODE_MAX_SUBAGENT_SPAWN_DEPTH": "2" } }
```

Credit: the depth-cap setting is from Anthropic's docs.

## Sources

- [sub-agents docs](https://code.claude.com/docs/en/sub-agents)
