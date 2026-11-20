# DEVX-081: Atuin Threads: searchable agent-session history, exposed to agents over MCP

## Summary

Atuin 18.24+ indexes Claude Code (and Codex, OpenCode) sessions, lets you resume or fork them across tools, and ships an MCP server so the agent can look up past investigations and why a decision was made. Capture is opt-in; sync is end-to-end encrypted, self-hostable, or local-only. Feasibility Medium, stage Assess, ~10 min.

## Details

- Enterprise caveat: transcripts contain secrets and code, so keep it local-only (no sync) until security signs off.
- PoC: `atuin resume` to try the history TUI, then `atuin mcp install claude`.
- Success metric: how often an agent reuses a prior investigation instead of starting from scratch on recurring bugs. Seen in 3 sources. Expires Feb 10, 2027.
- Also listed among the Nov 13 methods terms: encrypted, synced session history from Claude Code, Codex and OpenCode; you can resume or fork a session across tools, and reach it over MCP.

## Content

### 3. Atuin Threads: searchable agent-session history, exposed to agents over MCP — Enterprise feasibility: Medium | Stage: Assess

- What changed: Atuin 18.24+ indexes Claude Code (and Codex, OpenCode) sessions, lets you resume or fork them across tools, and ships an MCP server so the agent can look up past investigations and why a decision was made. Capture is opt-in; sync is end-to-end encrypted, self-hostable, or can stay local.
- Enterprise caveat: transcripts contain secrets and code. Keep it local-only (no sync) until your security team signs off.
- Effort: ~10 min.
- PoC: `atuin resume` to try the history TUI, then `atuin mcp install claude`.
- Success metric: how often an agent reuses a prior investigation instead of starting from scratch on recurring bugs.
- Sources: [Atuin blog](https://blog.atuin.sh/threads-agent-sessions/), [HN thread (212 pts)](https://news.ycombinator.com/item?id=50453637) | seen in 2 sources | expires Feb 10, 2027

## Sources

- [Atuin blog: Threads](https://blog.atuin.sh/threads-agent-sessions/)
- [HN thread (212 pts)](https://news.ycombinator.com/item?id=50453637)
