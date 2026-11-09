# DEVX-033: PreToolUse hook: block your email from going out in tool calls

## Summary

Claude Code adds the account email to every request and agents (incl. subagents) have put it in curl User-Agent headers; no setting to turn it off.

## Details

PoC (agent's own, untested; fails open without jq): {"hooks":{"PreToolUse":[{"hooks":[{"type":"command","command":"jq -c .tool_input | grep -qiF -f ~/.claude/never-send.txt && { echo 'Blocked: remove the personal detail; do not re-encode it.' >&2; exit 2; } || exit 0"}]}]}}. Success: no outbound tool calls containing employee emails. Stage Trial, feasibility Medium.

## Content

### Block your email  tool calls — Enterprise feasibility: Medium | Stage: Trial
- **What changed:** Claude Code adds the account email to every request. Agents, subagents included, have been seen putting it in curl User-Agent headers. There's no setting to turn this off and no reply from Anthropic yet.
- **Effort:** about 30 min.
- **PoC:** a PreToolUse hook that blocks any tool call containing a value listed in `~/.claude/never-send.txt`. The one-liner is mine and untested. It fails open if `jq` is missing.
```json
{"hooks":{"PreToolUse":[{"hooks":[{"type":"command","command":"jq -c .tool_input | grep -qiF -f ~/.claude/never-send.txt && { echo 'Blocked: remove the personal detail; do not re-encode it.' >&2; exit 2; } || exit 0"}]}]}}
```
- **Success metric:** no outbound tool calls containing employee emails.
- **Sources:** [issue #81138](https://github.com/anthropics/claude-code/issues/81138), [Tell HN post](https://news.ycombinator.com/item?id=50286306), [issue #95258 comment](https://github.com/anthropics/claude-code/issues/95258#issuecomment-6130024743). Seen in 4 sources. Expires Jan 30, 2027.

## Sources

- [issue #81138](https://github.com/anthropics/claude-code/issues/81138)
- [Tell HN](https://news.ycombinator.com/item?id=50286306)
- [issue #95258 comment](https://github.com/anthropics/claude-code/issues/95258#issuecomment-6130024743)