# DEVX-011: Make every file read go through the Read tool

## Summary

v2.1.299 added 'CLAUDE_CODE_DISABLE_FILE_MENTIONS'. Claude then gets only the paths of '@file' mentions and reads the files with its Read tool. The docs say Read deny rules apply to '@file' mentions only 'best-effort', so this makes deny rules and hooks always run.

## Details

Claude then gets only the paths of '@file' mentions and reads the files with its Read tool. The docs say Read deny rules apply to '@file' mentions only 'best-effort', so this makes deny rules and hooks always run. ….

## Sources

- [env vars](https://code.claude.com/docs/en/env-vars)
- [permissions](https://code.claude.com/docs/en/permissions)
- [v2.1.299 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.299)
