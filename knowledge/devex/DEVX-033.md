# DEVX-033: PreToolUse hook: block your email from going out in tool calls

## Summary

Claude Code adds the account email to every request and agents (incl. subagents) have put it in curl User-Agent headers; no setting to turn it off.

## Details

Success: no outbound tool calls containing employee emails. Stage Trial, feasibility Medium.

## Sources

- [issue #81138](https://github.com/anthropics/claude-code/issues/81138)
- [Tell HN](https://news.ycombinator.com/item?id=50286306)
- [issue #95258 comment](https://github.com/anthropics/claude-code/issues/95258#issuecomment-6130024743)
