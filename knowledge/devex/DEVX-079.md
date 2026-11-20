# DEVX-079: Stop the built-in Explore subagent from running on your most expensive model (Explore override, Sonnet main + Opus advisor)

## Summary

Per the subagent docs, the built-in Explore subagent runs on the main conversation's model (and on Opus when the main model is Fable), which quietly burns limits after switching to Fable 5.2 or Opus 5.5. Fix: a project/user subagent named Explore overrides the built-in with its own model. Pair with the advisor: Sonnet as main, Opus advising only at decision points. Feasibility High, stage Adopt, ~5 min.

## Details

- PoC: `claude --model sonnet --advisor opus`, or persist in `.claude/settings.json`: `{ "model": "sonnet", "advisorModel": "opus" }` (also `/advisor opus`). Fable as main only accepts a Fable advisor.
- Mod, Explore on Haiku (~2 min): save `.claude/agents/Explore.md` with `name: Explore`, `model: haiku`, `tools: Read, Grep, Glob`, body 'Search and summarize only. Never edit files. Return file paths with line numbers and a short answer.' (full file below).
- Mod, one model for every subagent / team cost cap (~1 min, Claude Code 2.1.257+): `{ "env": { "CLAUDE_CODE_SUBAGENT_MODEL": "sonnet", "CLAUDE_CODE_SUBAGENT_MODEL_FORCE": "1" } }` forces all subagents, Explore and teammates included, onto Sonnet.
- Success metric: `/usage` and cost per task over a week, before and after. Seen in 5+ sources. Expires Feb 10, 2027.
- Related: DEVX-003 (Haiku 5.5 for subagents), DEVX-009 (read-only Haiku researcher subagent), METH-134 (which Claude model to build with).
- For a wrapper or harness that launches Claude Code: set CLAUDE_CODE_SUBAGENT_MODEL together with CLAUDE_CODE_SUBAGENT_MODEL_FORCE=1 as environment variables from a preflight script, without touching the repo's settings.json. Bundle this with the subagent depth and concurrency caps (DEVX-077) and with pinning full model IDs in the model router, and log the model that actually ran. Without the two variables, the built-in Explore runs on Opus when the main model is Fable on a subscription. Effort about 15 minutes.

## Content

Context (Nov 12): a quiet day for releases. Claude Code was still 2.1.322 latest / 2.1.311 stable, with no new MCP server, Cursor or Aider releases.

### 1. Stop Explore from silently running on your most expensive model — Enterprise feasibility: High | Stage: Adopt

- What changed: per the current subagent docs, the built-in Explore subagent runs on your main conversation's model (and on Opus when your main model is Fable via a subscription or Console account). A wave of posts on Nov 11 pointed out that this quietly burns limits for anyone who switched to Fable 5.2 or Opus 5.5. The docs' fix is a project or user subagent named `Explore`, which overrides the built-in and keeps its own `model`.
- Pair it with the advisor: run Sonnet as the main model and let Opus advise only at decision points (`advisorModel` setting, `/advisor opus`, or `--advisor`). Fable as main only accepts a Fable advisor.
- Effort: ~5 min.
- PoC:

```bash
claude --model sonnet --advisor opus
```

  or persist it in `.claude/settings.json`: `{ "model": "sonnet", "advisorModel": "opus" }` (plus the Explore override in the mods below).
- Success metric: `/usage` and cost per task over a week, before and after.
- Sources: [subagent docs](https://code.claude.com/docs/en/sub-agents), [advisor docs](https://code.claude.com/docs/en/advisor), [model config](https://code.claude.com/docs/en/model-config), X posts by [@enjinxyz](https://x.com/enjinxyz/status/2120504313537589359) and [@bebuu_ai](https://x.com/bebuu_ai/status/2120402764715188533) | seen in 5+ sources | expires Feb 10, 2027

### Ready-to-use mods

- [Explore on Haiku (Claude Code)](https://code.claude.com/docs/en/sub-agents): codebase search runs on the cheap model no matter what your main model is. ~2 min. Save as `.claude/agents/Explore.md`:

```markdown
---
name: Explore
description: Fast read-only agent for searching and understanding the codebase. Use for file discovery and code search.
model: haiku
tools: Read, Grep, Glob
---
Search and summarize only. Never edit files. Return file paths with line numbers and a short answer.
```

- [One model for every subagent (team cost cap)](https://code.claude.com/docs/en/sub-agents): forces all subagents, Explore and teammates included, onto Sonnet. ~1 min (Claude Code 2.1.257+). In `.claude/settings.json`:

```json
{ "env": { "CLAUDE_CODE_SUBAGENT_MODEL": "sonnet", "CLAUDE_CODE_SUBAGENT_MODEL_FORCE": "1" } }
```

Credit: both mods come from Anthropic's docs.

## Sources

- [subagent docs](https://code.claude.com/docs/en/sub-agents)
- [advisor docs](https://code.claude.com/docs/en/advisor)
- [model config](https://code.claude.com/docs/en/model-config)
- [@enjinxyz on X](https://x.com/enjinxyz/status/2120504313537589359)
- [@bebuu_ai on X](https://x.com/bebuu_ai/status/2120402764715188533)
