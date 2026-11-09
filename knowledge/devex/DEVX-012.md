# DEVX-012: One instruction file for every agent (+ shared rules file)

## Summary

Claude Code reads 'AGENTS.md' only when there's no 'CLAUDE.md', '.claude/CLAUDE.md' or 'CLAUDE.local.md'.

## Details

A developer's personal 'CLAUDE.local.md' therefore silently drops the team's 'AGENTS.md'. Fix it by importing AGENTS.md S.md too), or by having a managed setting load both files.

## Content

- **[Shared rules file](https://code.claude.com/docs/en/memory)** (Claude Code + Cursor) keeps one source of truth for both tools. Effort ~2 min. Credit: Claude Code memory docs and @shtse8.
```bash
ln -s AGENTS.md CLAUDE.md   # or put "@AGENTS.md" as CLAUDE.md's first line
```

## 3. One instruction file for every agent: Enterprise feasibility High | Stage Adopt
- **What changed:** Claude Code reads `AGENTS.md` only when there's no `CLAUDE.md`, `.claude/CLAUDE.md` or `CLAUDE.local.md`. A developer's personal `CLAUDE.local.md` therefore silently drops the team's `AGENTS.md`. Fix it by importing AGENTS.md S.md too), or by having a managed setting load both files. Five sources this week.
- **Effort:** ~10 min.
- **PoC:** put `@AGENTS.md` as the first line of `CLAUDE.md`, or push this in user/managed settings (project settings ignore it):
```json
{ "pluginConfigs": { "cc-plugin-agents-md@builtin": { "options": { "instructionFiles": "claude-md-and-agents-md" } } } }
```
- **Success metric:** one rules file per repo; Claude Code and Cursor give the same answers to the same conventions.
- **Sources:** [Claude Code memory docs](https://code.claude.com/docs/en/memory), [Cursor rules](https://cursor.com/docs/context/rules), [@shtse8 on X](https://x.com/shtse8/status/2109983383405355416), [@PearEsmaeil on X](https://x.com/PearEsmaeil/status/2109997068760531014)

## Sources

- [Claude Code memory docs](https://code.claude.com/docs/en/memory)
- [Cursor rules](https://cursor.com/docs/context/rules)
- [@shtse8 on X](https://x.com/shtse8/status/2109983383405355416)
- [@PearEsmaeil on X](https://x.com/PearEsmaeil/status/2109997068760531014)