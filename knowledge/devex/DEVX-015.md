# DEVX-015: Pin a 1h prompt cache on API-key seats, then measure it

## Summary

v2.1.300 splits cache writes into 5m and 1h in its telemetry ('cache_creation_5m_tokens' and 1h).

## Details

'promptCacheTtl: 1h' keeps the main conversation cached through coffee breaks, and subagents stay on 5m. A 1h write costs more per write, so it's the wrong choice for short CI jobs.

## Sources

- [prompt caching docs](https://code.claude.com/docs/en/prompt-caching)
- [settings reference](https://code.claude.com/docs/en/settings-reference#promptcachettl)
- [issue #102276](https://github.com/anthropics/claude-code/issues/102276)
- [claude-code-templates PR …](https://github.com/davila7/claude-code-templates/pull/1178)
