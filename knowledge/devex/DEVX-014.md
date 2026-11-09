# DEVX-014: Monthly stale-rules check

## Summary

(Claude Code) flags outdated or conflicting CLAUDE.md, AGENTS.md, skills and subagents.

## Content

- **[Monthly stale-rules check](https://code.claude.com/docs/en/memory)** (Claude Code) flags outdated or conflicting CLAUDE.md, AGENTS.md, skills and subagents. It proposes edits and changes nothing until you approve. Needs v2.1.283+. Effort ~2 min. Credit: Claude Code memory docs.
```
/doctor prompt-audit
/doctor prompt-audit .claude/skills/deploy
```

## Sources

- [Claude Code memory docs](https://code.claude.com/docs/en/memory)
