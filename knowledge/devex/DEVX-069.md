# DEVX-069: Claude Code 2.1.321/2.1.322: security fixes, mods permission change, Fable 5.2 default, gateway changes

## Summary

2.1.321 and 2.1.322 shipped overnight (stable still 2.1.311). 2.1.321 fixes MCP OAuth sending refresh tokens to another host on redirect, a read-only Bash command running outside the sandbox without a prompt, and deny rules not covering files written by cp/mv into a folder. Update with claude install 2.1.322.

## Details

- Security fixes in 2.1.321 (not yet on stable 2.1.311): MCP OAuth secrets leaked to a redirect host; read-only Bash ran unsandboxed without a prompt; deny rules missed files cp/mv wrote into a folder. Run `claude install 2.1.322`.
- Mods (in-process JavaScript plugins): mods Claude writes now turn on without asking in auto and bypass modes, even with managed allowUnsandboxedCommands: false; a mod's own tool calls no longer raise a permission prompt even under ask rules. Deny rules and org policy still apply, so treat ask as a convenience, not a guard. allowManagedModsOnly (reported Oct 20) is the hard stop; re-run its --plugin-dir refusal test after upgrading.
- Model default: Claude Fable 5.2 is now the default Fable model ($8 input / $40 output per million tokens). Saved Fable 5.1 picks move to it right away on Pro and Max, and on Team/Enterprise once the org allows it. If evals aren't done, pin with /model claude-fable-5-1.
- Claude apps gateway: Bedrock, Vertex and Foundry upstreams now ignore ANTHROPIC_*_BASE_URL, so set base_url on the upstream; policy_mode: layered now adds up managed MCP servers across every matching policy.
- Advisory CVE-2026-88968 (high): race in the Edit tool on macOS let sandboxed code overwrite a file outside the workspace; fixed in 2.1.251, nothing to do if current.

## Content

**Claude Code release notes, Tue Nov 10** (Claude Code 2.1.321 and 2.1.322 shipped overnight; latest is 2.1.322, stable is still 2.1.311. No new MCP servers, Inspector, Aider or Cursor releases.)

**Breaking-change alerts**
- **Update to Claude Code 2.1.321 or later.** It fixes MCP OAuth sending secrets such as refresh tokens to another host when a server redirected, a read-only Bash command running outside the sandbox without a prompt, and deny rules not applying to files that `cp` or `mv` write into a folder. The stable channel (2.1.311) doesn't have these fixes yet. Run `claude install 2.1.322`. [v2.1.321 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.321)
- **Mods (in-process JavaScript plugins) changed how permissions apply to them.** Mods that Claude writes now turn on without asking in auto and bypass modes, even with managed `allowUnsandboxedCommands: false`. A mod's own tool calls no longer raise a permission prompt, even under your `ask` rules. Deny rules and org policy still apply, so treat `ask` as a convenience, not a guard. The `allowManagedModsOnly` setting (reported Oct 20) is the hard stop. Re-run its `--plugin-dir` refusal test after you upgrade. [v2.1.321 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.321), [mods overview](https://code.claude.com/docs/en/plugins/mods/overview)
- **Model default moved.** Claude Fable 5.2 is now the default Fable model, at $8 input and $40 output per million tokens. Saved Fable 5.1 picks move to it right away on Pro and Max, and on Team and Enterprise once your org allows it. If your evals aren't done, pin the old one with `/model claude-fable-5-1`. [Anthropic announcement](https://www.anthropic.com/claude-fable-and-mythos-5-2)
- **Claude apps gateway users:** Bedrock, Vertex and Foundry upstreams now ignore the `ANTHROPIC_*_BASE_URL` variables, so set `base_url` on the upstream instead. Also, `policy_mode: layered` now adds up managed MCP servers across every matching policy, so the gateway serves more of them after the upgrade.
- **New advisory, nothing to do if you're current.** [CVE-2026-88968](https://github.com/advisories/GHSA-5xjx-9qx6-jcrv) is a high-severity race in the Edit tool on macOS. Code running inside the sandbox could get Edit to overwrite a file outside the workspace. It's fixed in 2.1.251.

## Sources

- [v2.1.321 notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.321)
- [mods overview](https://code.claude.com/docs/en/plugins/mods/overview)
- [Anthropic: Fable and Mythos 5.2](https://www.anthropic.com/claude-fable-and-mythos-5-2)
- [CVE-2026-88968](https://github.com/advisories/GHSA-5xjx-9qx6-jcrv)
