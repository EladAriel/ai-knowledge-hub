# DEVX-091: Post-upgrade health check: /status now lists broken config

## Summary

In 2.1.327, `/status` lists broken agent, skill, command and output-style files, keybinding errors, an unavailable sandbox, ignored permission settings, and hook matchers that never match. Since 2.1.326 it also shows when your provider or a variable such as `DISABLE_TELEMETRY` turns features off. Pair it with a search for hooks that print `"decision": "block"`, which hold in more cases since 2.1.326. Enterprise feasibility: High. Stage: Adopt. Effort: about 5 minutes.

## Details

Practical PoC:
```bash
claude update && claude   # then type: /status
grep -rn '"decision"' ~/.claude/hooks .claude/hooks 2>/dev/null
```
Success metric: zero broken or ignored entries in `/status` on a reference machine, and no surprise hook blocks in the first week. Seen in 3 sources. Expires Feb 16, 2027.

## Sources

- [2.1.327 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.327)
- [2.1.326 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.326)
- [@alexmichael on X](https://x.com/alexmichael/status/2122832083298963706)
