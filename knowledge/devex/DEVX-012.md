# DEVX-012: One instruction file for every agent (+ shared rules file)

## Summary

Claude Code reads 'AGENTS.md' only when there's no 'CLAUDE.md', '.claude/CLAUDE.md' or 'CLAUDE.local.md'.

## Details

A developer's personal 'CLAUDE.local.md' therefore silently drops the team's 'AGENTS.md'. Fix it by importing AGENTS.md from CLAUDE.md (Cursor reads AGENTS.md too), or by having a managed setting load both files. ….

## Sources

- [Claude Code memory docs](https://code.claude.com/docs/en/memory)
- [Cursor rules](https://cursor.com/docs/context/rules)
- [@shtse8 on X](https://x.com/shtse8/status/2109983383405355416)
- [@PearEsmaeil on X](https://x.com/PearEsmaeil/status/2109997068760531014)
