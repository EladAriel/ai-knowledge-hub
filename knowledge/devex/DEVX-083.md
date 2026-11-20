# DEVX-083: Claude Code 2.1.323 / 2.1.325 breaking-change alerts (sandboxed Bash prompts again, unknown models assumed 1M, v1 MCP client gone, scheduled skills ask)

## Summary

2.1.325 (Nov 13, 22:40 Israel time): sandbox.autoAllowBashIfSandboxed now defaults to false, read-only git commands ask outside trusted repos, scheduled tasks and /loop ask before a skill that declares allowed-tools or hooks, managed pluginDigests is ignored, plus zstd and Bash/sandbox security fixes. 2.1.323 (Nov 13, 00:12): unrecognized model IDs are assumed to have a 1M window, org settings no longer use an ALL_PROXY-only proxy, the v1 MCP client is removed, subagentStatusLine removed. Latest 2.1.325, stable still 2.1.311.

## Details

- 2.1.325: `sandbox.autoAllowBashIfSandboxed` defaults to `false` (was `true` before v2.1.324), so sandboxed commands go through normal allow rules and permission mode (see DEVX-085). Read-only git commands now ask in a repo that isn't the project's or a trusted one (use `--add-dir`). Scheduled tasks and `/loop` ask before running a skill that declares `allowed-tools` or hooks. Managed `pluginDigests` deprecated and ignored. Fixes a zstd decoding security issue and several Bash permission and sandbox gaps.
- 2.1.323: an unrecognized model ID is assumed to have a 1M window, not 200K, so sessions on smaller gateway models can fail every turn instead of compacting (see DEVX-086). Org settings and policy requests no longer use a proxy set only by `ALL_PROXY`; set `HTTPS_PROXY`. `MCP_SDK_GENERATION=v1` now runs the v2 client in a compatibility mode. `subagentStatusLine` removed; a plugin's `agent` setting deprecated. Neither release is on `stable` yet.
- Mod, unattended skill allow for `/loop` and scheduled tasks (~1 min): allow only reviewed skills by name in `.claude/settings.json`: `{ "permissions": { "allow": ["Skill(release-notes)"] } }` (replace with your skill's name).
- For wrappers that run Claude Code unattended: raise the minimum supported version to 2.1.325, and add a preflight rule that an unattended run waiting on a permission prompt fails fast, because 2.1.325 made sandboxed Bash and read-only git in untrusted repos prompt again.
- Related: DEVX-069 (2.1.321/2.1.322 alerts). Nov 18 update: the 2.1.326/2.1.327 alerts are in DEVX-088.

## Content

Context (Nov 15): Claude Code shipped 2.1.323 and 2.1.325 since Thursday; latest is now 2.1.325, stable is still 2.1.311. The MCP Inspector's 2.15.0 security release had been missed in the previous check. Nothing new from the MCP servers, SDKs, Aider or Cursor.

### Breaking-change alerts

- **Claude Code 2.1.325: sandboxed Bash prompts again by default.** Released Nov 13 at 22:40 Israel time ([release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.325)). `sandbox.autoAllowBashIfSandboxed` now defaults to `false` (it was `true` before v2.1.324), so sandboxed commands go through your normal allow rules and permission mode. If your team relied on the sandbox for prompt-free Bash, see DEVX-085. In the same release: read-only git commands now ask in a repo that isn't the project's or one you trusted (use `--add-dir`). Scheduled tasks and `/loop` now ask before running a skill that declares `allowed-tools` or hooks (add `Skill(name)` to `permissions.allow`). Managed `pluginDigests` is deprecated and ignored. Also fixes a zstd decoding security issue and several Bash permission and sandbox gaps.
- **Claude Code 2.1.323 (Nov 13, 00:12 Israel time) changes things for gateway and proxy users** ([release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.323)). A model ID Claude Code doesn't recognize is now assumed to have a 1M window, not 200K, so sessions on smaller gateway models can fail every turn instead of compacting (see DEVX-086). Org settings and policy requests no longer use a proxy set only by `ALL_PROXY`, so set `HTTPS_PROXY`. The v1 MCP client is gone: `MCP_SDK_GENERATION=v1` now runs the v2 client in a compatibility mode. The `subagentStatusLine` setting is removed, and a plugin's `agent` setting is deprecated. Neither release is on `stable` yet.

### Ready-to-use mod

- [Unattended skill allow for `/loop` and scheduled tasks](https://github.com/anthropics/claude-code/releases/tag/v2.1.325): since 2.1.325, a scheduled run stops and asks before a skill that declares `allowed-tools` or hooks. Allow only the skills you've reviewed, by name. ~1 min. In `.claude/settings.json` (replace with your skill's name):

```json
{ "permissions": { "allow": ["Skill(release-notes)"] } }
```

Credit: based on Anthropic's docs and the 2.1.325 release notes.

## Sources

- [2.1.325 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.325)
- [2.1.323 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.323)
- [2.1.326 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.326)
- [2.1.327 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.327)
