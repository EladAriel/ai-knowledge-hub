# DEVX-060: Claude Code 2.1.319 (latest/next): auto mode fails closed without the server check; decide CLAUDE_CODE_AUTO_MODE_SERVER

## Summary

2.1.319 (released Nov 6, 19:04 Israel time; stable still 2.1.311) no longer falls back to the built-in auto-mode classifier when telemetry or feature flags are off, including behind LLM gateways: calls the server can't check are asked about or denied, and claude -p in auto mode now exits 1 when actions are refused. Pick a policy with CLAUDE_CODE_AUTO_MODE_SERVER=0 (keep built-in classifier) or =1 (force server-side check).

## Details

Breaking: no built-in fallback when DISABLE_TELEMETRY / CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC / CLAUDE_CODE_DISABLE_FEATURE_FLAGS are set or behind gateways. CLAUDE_CODE_AUTO_MODE_SERVER=1 forces the server check even with CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS (if managed settings set the latter they must set =1 too). Bedrock, Vertex and Foundry unchanged. claude -p auto mode exits 1 (text and JSON) instead of 0 when refused for lack of a safety check. A project file or plugin can no longer re-enable the server-side check once switched off outside the project.
Also in 2.1.319: permissions.denyInsteadOfPrompting; CLAUDE_CODE_DISABLE_FEATURE_FLAGS (stops flag fetching without disabling telemetry); MCP tasks in the terminal (Nov 9 correction: the env var is CLAUDE_CODE_DISABLE_MCP_TASK_BACKGROUND, not CLAUDE_CODE_DISABLE_MCP_TASKS; it does not turn MCP tasks off, it makes Claude Code wait for the task inside the tool call instead of moving it to the background); Bash deny/ask rules catch quoted words; a session's exact Bash/PowerShell ask rule is refused when a broader deny covers it; `which` with unexpected flags asks; --add-dir directories register plugin marketplaces only after their own trust dialog; fixes a sandbox escape when creating a worktree and a Bash permission bypass via a crafted env prefix; fixes older-handshake MCP servers.
PoC: npm view @anthropic-ai/claude-code dist-tags (expect latest=2.1.319 next=2.1.319 stable=2.1.311); claude --version; export CLAUDE_CODE_AUTO_MODE_SERVER=0 or =1.
Success metric: fleet latest/next is 2.1.319; /status Auto mode server row matches policy; CI -p jobs treat exit 1 as a refused run.
Org challenge: gateway teams relying on the silent fallback will see more prompts/denials unless they set =0. Unverified #108258 claims Remote Control --spawn sessions never start a turn after 2.1.309 -> 2.1.319.
Feasibility High, stage Adopt; seen in 5 sources. Includes the related breaking-change alert.

## Content

- **Claude Code 2.1.319 (npm `latest`=`next`) no longer falls back to the built-in auto-mode classifier when telemetry or feature flags are off, including behind LLM gateways.** GitHub release Friday Nov 6 at 19:04 Israel time ([v2.1.319](https://github.com/anthropics/claude-code/releases/tag/v2.1.319)). Calls the server cannot check are asked about or denied. Set `CLAUDE_CODE_AUTO_MODE_SERVER=0` to keep the built-in classifier; set `CLAUDE_CODE_AUTO_MODE_SERVER=1` to force the server-side check even with `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` (if managed settings set the latter, they must set the `1` too). Bedrock, Vertex and Foundry are unchanged. `claude -p` in auto mode now exits `1` (text and JSON) when actions are refused because no safety check is available; it previously exited `0`. A project file or plugin can no longer turn the server-side check back on once it has been switched off outside the project. **Stable is still 2.1.311.**

### 2. Upgrade Claude Code `latest`/`next` to 2.1.319 and decide `AUTO_MODE_SERVER` for gateway and no-telemetry fleets — Enterprise feasibility: High | Stage: Adopt
- **What changed:** first Claude Code release since Thursday (was 2.1.318). Besides the auto-mode change, 2.1.319 adds `permissions.denyInsteadOfPrompting`, `CLAUDE_CODE_DISABLE_FEATURE_FLAGS` (stops feature-flag fetching without turning off telemetry), MCP tasks in the terminal (opt out with `CLAUDE_CODE_DISABLE_MCP_TASKS=1`), and permission hardening: Bash deny and ask rules now catch quoted words; a session’s exact Bash or PowerShell ask rule is refused when a broader deny covers the command; `which` with unexpected flags now asks; `--add-dir` directories register plugin marketplaces only after that directory’s own trust dialog. It also fixes a sandbox escape when creating a worktree and a Bash permission bypass via a crafted environment prefix. Older-handshake MCP servers that failed to connect or returned empty results are fixed.
- **How it works:** pin or update the `latest`/`next` channel to 2.1.319. On LLM gateways or machines with `DISABLE_TELEMETRY` / `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` / `CLAUDE_CODE_DISABLE_FEATURE_FLAGS`, pick an auto-mode policy: leave the new fail-closed behavior, set `CLAUDE_CODE_AUTO_MODE_SERVER=0` to keep the built-in classifier, or set `CLAUDE_CODE_AUTO_MODE_SERVER=1` to force the server-side check. Bedrock, Vertex and Foundry do not change. Stable remains 2.1.311 until Anthropic promotes it.
- **Effort:** ~15 min
- **PoC:**
```bash
npm view @anthropic-ai/claude-code dist-tags
# expect: latest=2.1.319 next=2.1.319 stable=2.1.311
claude --version
# export CLAUDE_CODE_AUTO_MODE_SERVER=0   # keep built-in classifier
# export CLAUDE_CODE_AUTO_MODE_SERVER=1   # force server-side check even with DISABLE_EXPERIMENTAL_BETAS
# Headless auto-mode runs that used to exit 0 when no safety check was available now exit 1.
```
- **Success metric:** fleet `latest`/`next` resolves to 2.1.319; `/status` Auto mode server row matches the intended policy; CI `-p` jobs treat exit 1 as a refused auto-mode run rather than success.
- **Org challenge:** gateway teams that relied on the silent built-in classifier fallback will see more prompts or denials unless they set `AUTO_MODE_SERVER=0`. Unverified [#108258](https://github.com/anthropics/claude-code/issues/108258) claims Remote Control `--spawn` sessions attach but never start a turn after 2.1.309 → 2.1.319.
- **Sources:** [v2.1.319](https://github.com/anthropics/claude-code/releases/tag/v2.1.319), [changelog](https://code.claude.com/docs/en/changelog), [auto-mode classifier billing](https://code.claude.com/docs/en/auto-mode-classifier-billing), [npm dist-tags](https://registry.npmjs.org/-/package/@anthropic-ai/claude-code/dist-tags) | seen in 5 sources

**Breaking-change alerts**
- No new breaking changes or CVEs. One correction to the previous day's note: the 2.1.319 env var is `CLAUDE_CODE_DISABLE_MCP_TASK_BACKGROUND`, not `CLAUDE_CODE_DISABLE_MCP_TASKS`. It doesn't turn MCP tasks off; it makes Claude Code wait for the task inside the tool call instead of moving it to the background. [v2.1.319 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.319)

## Sources

- [v2.1.319](https://github.com/anthropics/claude-code/releases/tag/v2.1.319)
- [changelog](https://code.claude.com/docs/en/changelog)
- [auto-mode classifier billing](https://code.claude.com/docs/en/auto-mode-classifier-billing)
- [npm dist-tags](https://registry.npmjs.org/-/package/@anthropic-ai/claude-code/dist-tags)
- [#108258](https://github.com/anthropics/claude-code/issues/108258)
