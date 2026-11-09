# DEVX-039: open-effort: automatic effort level per request (Claude Code plugin)

## Summary

Haiku picks an effort level per request, raised after repeated failed checks; Explore subagents run on Haiku at low effort.

## Details

claude plugin marketplace add JakkapatB/open-effort && claude plugin install open-effort@open-effort. Author's own test (61 sessions): cost -4–11%, one Explore subagent run $0.41 -> $0.09. Small, self-reported sample; new MIT repo (9 stars), so try on one team first.

## Content

**[open-effort](https://github.com/JakkapatB/open-effort)** (~10 min) is a Claude Code plugin that sets the effort level automatically.
- Haiku picks an effort level for each request, and the level goes up after repeated failed checks.
- Explore subagents run on Haiku at low effort.
- In the author's test of 61 sessions, cost fell 4–11%, and one Explore run dropped from $0.41 to $0.09.
- That's a small sample from a new MIT repo, so try it on one team first.
```bash
claude plugin marketplace add JakkapatB/open-effort && claude plugin install open-effort@open-effort
```

## Sources

- [open-effort](https://github.com/JakkapatB/open-effort)