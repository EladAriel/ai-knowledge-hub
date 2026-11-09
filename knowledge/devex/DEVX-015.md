# DEVX-015: Pin a 1h prompt cache on API-key seats, then measure it

## Summary

v2.1.300 splits cache writes into 5m and 1h in its telemetry ('cache_creation_5m_tokens' and 1h).

## Details

'promptCacheTtl: 1h' keeps the main conversation cached through coffee breaks, and subagents stay on 5m. A 1h write costs more per write, so it's the wrong choice for short CI jobs.

## Content

## 2. Pin a 1h prompt cache on API-key seats, then measure it: Enterprise feasibility High | Stage Trial
- **What changed:** v2.1.300 splits cache writes into 5m and 1h in its telemetry (`cache_creation_5m_tokens` and `cache_creation_1h_tokens`), so you can finally see which one you're paying for.
- **How it works:** `promptCacheTtl: "1h"` keeps the main conversation cached through coffee breaks, and subagents stay on 5m. A 1h write costs more per write, so it's the wrong choice for short CI jobs.
- **Effort:** ~10 min.
- **PoC (settings.json):**
```json
{ "promptCacheTtl": "1h", "subagentPromptCacheTtl": "5m" }
```
Verify: `claude -p "hello" --output-format json | jq '.usage.cache_creation'`
- **Success metric:** the `ephemeral_1h_input_tokens` count is above 0, and the cache hit ratio in `/usage` goes up over two weeks.
- **Sources:** [prompt caching docs](https://code.claude.com/docs/en/prompt-caching), [settings reference](https://code.claude.com/docs/en/settings-reference#promptcachettl), [issue #102276](https://github.com/anthropics/claude-code/issues/102276), [claude-code-templates PR #1178](https://github.com/davila7/claude-code-templates/pull/1178)

## Sources

- [prompt caching docs](https://code.claude.com/docs/en/prompt-caching)
- [settings reference](https://code.claude.com/docs/en/settings-reference#promptcachettl)
- [issue #102276](https://github.com/anthropics/claude-code/issues/102276)
- [claude-code-templates PR #1178](https://github.com/davila7/claude-code-templates/pull/1178)