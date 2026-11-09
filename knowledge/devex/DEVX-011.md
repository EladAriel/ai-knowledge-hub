# DEVX-011: Make every file read go through the Read tool

## Summary

Claude then gets only the paths of '@file' mentions and reads the files with its Read tool. The docs say Read deny rules apply to '@file' mentions only 'best-effort', so this makes deny rules and hooks always run.

## Details

Claude then gets only the paths of '@file' mentions and reads the files with its Read tool. The docs say Read deny rules apply to '@file' mentions only 'best-effort', so this makes deny rules and hooks always run.

## Content

## 2. Make every file read go through the Read tool: Enterprise feasibility High | Stage Trial
- **What changed:** v2.1.299 added `CLAUDE_CODE_DISABLE_FILE_MENTIONS`. Claude then gets only the paths of `@file` mentions and reads the files with its Read tool. The docs say Read deny rules apply to `@file` mentions only "best-effort", so this makes deny rules and hooks always run. The same release added idle compaction: a conversation over 200K tokens that sits idle about 54 minutes is summarised before its prompt cache expires.
- **Effort:** ~5 min.
- **PoC (settings.json):**
```json
{ "env": { "CLAUDE_CODE_DISABLE_FILE_MENTIONS": "1", "CLAUDE_CODE_IDLE_COMPACT_MIN_TOKENS": "150000" } }
```
- **Success metric:** no denied-path content shows up in transcripts; fewer full cache re-reads after breaks.
- **Sources:** [env vars](https://code.claude.com/docs/en/env-vars), [permissions](https://code.claude.com/docs/en/permissions), [v2.1.299 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.299)

## Sources

- [env vars](https://code.claude.com/docs/en/env-vars)
- [permissions](https://code.claude.com/docs/en/permissions)
- [v2.1.299 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.299)