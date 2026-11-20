# DEVX-085: Re-decide sandbox auto-allow after 2.1.325, and lock it in managed settings so a repo can't flip it

## Summary

Since 2.1.325 a sandboxed Bash command no longer runs without a prompt by default. The docs say a repo's own .claude/settings.json can still set autoAllowBashIfSandboxed even when the sandbox is admin-required, so pick true or false per team and set it in managed settings. true runs sandboxed commands without a prompt but deny and content-scoped ask rules (e.g. Bash(git push *)) still apply; false sends them through allow rules and permission mode. Feasibility High, stage Adopt, ~5 min.

## Details

- PoC: in `/etc/claude-code/managed-settings.json` (Linux) or `/Library/Application Support/ClaudeCode/managed-settings.json` (macOS): `{ "sandbox": { "enabled": true, "autoAllowBashIfSandboxed": false } }` (use `true` for the old prompt-free behavior). Then `/status` should show `Setting sources` = `Enterprise managed settings (file)`.
- Success metric: permission prompts per session before and after the upgrade, and no repo can change the value (`/sandbox` should say the setting is overridden).
- For unattended runs: the new default (prompts on) is a stall risk, so those runs should fail fast on a permission prompt instead of waiting.
- Seen in 4 sources. Expires Feb 13, 2027. Nov 18 update: 2.1.326 added `sandbox.filesystem.allowWrite`; the related alerts are in DEVX-088.

## Content

### 1. Re-decide sandbox auto-allow, and lock it so a repo can't flip it — Enterprise feasibility: High | Stage: Adopt

- What changed: since 2.1.325, a sandboxed Bash command no longer runs without a prompt by default. The docs also say that even when the sandbox is admin-required, a repo's own `.claude/settings.json` can still set `autoAllowBashIfSandboxed`. The fix is to set the key in managed settings.
- How it works: `true` runs sandboxed commands without a prompt, but `deny` rules and content-scoped `ask` rules such as `Bash(git push *)` still apply. `false` sends them through your allow rules and permission mode. Pick one per team and enforce it centrally.
- Effort: ~5 min.
- PoC (`/etc/claude-code/managed-settings.json` on Linux, or `/Library/Application Support/ClaudeCode/managed-settings.json` on macOS). Use `true` if you want the old prompt-free behavior:

```json
{ "sandbox": { "enabled": true, "autoAllowBashIfSandboxed": false } }
```

  Then run `/status` and check that `Setting sources` shows `Enterprise managed settings (file)`.
- Success metric: permission prompts per session before and after the upgrade, and no repo that can change the value (`/sandbox` should say the setting is overridden).
- Sources: [2.1.325 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.325), [settings reference](https://code.claude.com/docs/en/settings-reference#sandbox-autoallowbashifsandboxed), [sandboxing docs](https://code.claude.com/docs/en/sandboxing), [managed settings](https://code.claude.com/docs/en/managed-settings), [X post by @linklin63793](https://x.com/linklin63793/status/2121380727518556568) | seen in 4 sources | expires Feb 13, 2027

## Sources

- [2.1.325 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.325)
- [settings reference](https://code.claude.com/docs/en/settings-reference#sandbox-autoallowbashifsandboxed)
- [sandboxing docs](https://code.claude.com/docs/en/sandboxing)
- [managed settings](https://code.claude.com/docs/en/managed-settings)
- [@linklin63793 on X](https://x.com/linklin63793/status/2121380727518556568)
- [2.1.326 notes (allowWrite)](https://github.com/anthropics/claude-code/releases/tag/v2.1.326)
