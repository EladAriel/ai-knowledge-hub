# DEVX-025: One skills folder for Claude Code and Cursor

## Summary

Anthropic gave the Agent Skills standard to the Linux Foundation's Agentic AI Foundation (AAIF).

## Content

### 5. One skills folder for Claude Code and Cursor — Enterprise feasibility: High | Stage: Trial
- **What changed:** Anthropic gave the Agent Skills standard to the Linux Foundation's Agentic AI Foundation (AAIF), which also hosts MCP. Cursor already reads `.claude/skills/`, so one folder serves both tools.
- **Effort:** ~30 min
- **PoC:** use only the spec's frontmatter fields, so the skill works everywhere.
```yaml
# .claude/skills/<name>/SKILL.md
---
name: <name>
description: <one line saying WHEN to use it>
license: Apache-2.0
metadata:
  owner: platform-team
---
```
- **Success metric:** the same skill triggers in both tools, with one copy per repo.
- **Sources:** [Anthropic](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation), [Simon Willison](https://simonwillison.net/2026/Oct/22/donating-agent-skills/), [Cursor skills docs](https://cursor.com/docs/skills) | seen in 6 sources

## Sources

- [Anthropic](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation)
- [Simon Willison](https://simonwillison.net/2026/Oct/22/donating-agent-skills/)
- [Cursor skills docs](https://cursor.com/docs/skills)
