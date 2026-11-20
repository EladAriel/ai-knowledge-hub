# DEVX-086: Gateway users: tell Claude Code your model's real context window (2.1.323 assumes 1M for unknown model IDs)

## Summary

Since 2.1.323 an unrecognized model ID (a gateway alias such as my-gateway-opus, or another vendor's model) is assumed to have 1M tokens; on a smaller model Claude Code stops compacting in time and the session fails until /clear. Startup warning: 'Model "…" isn't recognized · context assumed to be 1m tokens'. Fix: map the alias with modelOverrides, or set CLAUDE_CODE_MAX_CONTEXT_TOKENS, or CLAUDE_CODE_DISABLE_1M_CONTEXT=1 to keep 200K everywhere. Feasibility High, stage Adopt, ~5 min.

## Details

- PoC (managed or user `settings.json`, use your model's real window): `{ "env": { "CLAUDE_CODE_MAX_CONTEXT_TOKENS": "200000" } }`
- Success metric: zero "prompt is too long" or failed turns on gateway sessions after the upgrade, and the startup warning gone.
- Seen in 4 sources. Expires Feb 13, 2027.
- For a model router that launches Claude Code: pass an explicit context window for each model it selects. `CLAUDE_CODE_MAX_CONTEXT_TOKENS` only applies to IDs that start with `claude-`; for other IDs use `CLAUDE_CODE_DISABLE_1M_CONTEXT=1`. Together with forcing the subagent model (DEVX-079), this gives a real context cap. About 15 minutes.

## Content

### 2. Gateway users: tell Claude Code your model's real context window — Enterprise feasibility: High | Stage: Adopt

- What changed: since 2.1.323, an unrecognized model ID (a gateway alias such as `my-gateway-opus`, or another vendor's model) is assumed to have 1M tokens. On a smaller model, Claude Code stops compacting in time and the session fails until `/clear`. Look for the startup warning `Model "…" isn't recognized · context assumed to be 1m tokens`.
- How it works: map the alias to a known model with `modelOverrides`, or set the real window with `CLAUDE_CODE_MAX_CONTEXT_TOKENS`. To keep the old 200K for everything, set `CLAUDE_CODE_DISABLE_1M_CONTEXT=1`.
- Effort: ~5 min.
- PoC (in managed or user `settings.json`; use your model's real window):

```json
{ "env": { "CLAUDE_CODE_MAX_CONTEXT_TOKENS": "200000" } }
```

- Success metric: zero "prompt is too long" or failed turns on gateway sessions after the upgrade, and the startup warning gone.
- Sources: [2.1.323 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.323), [model config: correct the window for a gateway ID](https://code.claude.com/docs/en/model-config#correct-the-window-for-a-gateway-or-custom-model-id), [env vars](https://code.claude.com/docs/en/env-vars), [X post by @HimanshuRawal05](https://x.com/HimanshuRawal05/status/2121118066906149157) | seen in 4 sources | expires Feb 13, 2027

## Sources

- [2.1.323 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.323)
- [model config: gateway window](https://code.claude.com/docs/en/model-config#correct-the-window-for-a-gateway-or-custom-model-id)
- [env vars](https://code.claude.com/docs/en/env-vars)
- [@HimanshuRawal05 on X](https://x.com/HimanshuRawal05/status/2121118066906149157)
