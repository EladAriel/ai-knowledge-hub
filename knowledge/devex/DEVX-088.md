# DEVX-088: Claude Code 2.1.326 / 2.1.327 breaking-change alerts (start mode, hooks, sandbox writes, plugins, plus MCP CVEs)

## Summary

Claude Code released 2.1.326 on Nov 17 at 00:11 and 2.1.327 on Nov 18 at 01:17, Israel time, so latest is now 2.1.327. Stable is still 2.1.311. 2.1.326 changes start mode, hook blocking, sandbox writes, plugins, self-hosted `gh api`, and managed autoMode.environment. 2.1.327 fixes `claude mcp add` / `remove --scope project` deleting other top-level keys from `.mcp.json`, and stops a nested `claude` under `forceLoginOrgUUID` inheriting `CLAUDE_CODE_OAUTH_SCOPES`. Also: Kubeshark and code-review-mcp-server CVEs, and MCP Java SDK 2.2.0 deprecations.

## Details

2.1.326 changes that can break existing setups ([release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.326)):
- Start mode: orgs on the HIPAA configuration now start in auto mode instead of Manual. Any session with no mode set also starts in auto if the org policy hasn't loaded. See DEVX-090.
- Hooks: a hook's `"decision": "block"` now takes effect in more cases, so a hook that always prints a decision may start blocking calls. See DEVX-091.
- Sandbox: sandboxed commands can no longer write to some sensitive folders in the home directory. Re-allow the ones you need with `sandbox.filesystem.allowWrite` (mod below).
- Auto mode behind gateways and proxies: an upcoming release will stop falling back to the billed auto-mode safety check. After that, those actions will prompt or be denied.
- Plugins: plugins that used to be refused for a malformed display field in `plugin.json` now load, including their hooks and MCP servers. Re-check the plugins you deploy.
- Self-hosted runners: a runner without `gh` now gets a built-in `gh api` that goes through Anthropic using your GitHub sign-in. Turn it off with `--use-anthropic-gh false`.
- Desktop and Agent SDK: a managed `autoMode.environment` list without `"$defaults"` now replaces the built-in entries there too.

2.1.327 ([release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.327)): if you used `claude mcp add` or `claude mcp remove --scope project`, check `.mcp.json` for missing top-level keys such as `$schema`. Set `CLAUDE_CODE_OAUTH_SCOPES` explicitly where a nested `claude` under `forceLoginOrgUUID` needs it.

MCP server CVEs, fixed upstream: Kubeshark `kubeshark mcp` CVE-2026-129236 (high, 7.2, argument injection in `start_kubeshark` that can lead to a cluster takeover) and CVE-2026-129235 (medium, arbitrary file write in `download_file`) — upgrade to v53.4.0. `code-review-mcp-server` CVE-2026-68934 (high, command injection) — upgrade to 1.5.3. MCP Java SDK 2.2.0 deprecates the APIs that start roots, sampling and logging (SEP-2577); `McpTransportContext` also lost its content-based `equals`/`hashCode`.

The Inspector, MCP servers, the TypeScript and Python SDKs, Aider and Cursor's changelog have nothing new since Sunday. Related: DEVX-083 (2.1.323/325 alerts).

Ready-to-use mods:
- Re-allow a CLI's write folder after the 2.1.326 sandbox tightening, about 2 minutes, for tools like `kubectl`. List only the paths that broke. In user or managed settings: `{ "sandbox": { "filesystem": { "allowWrite": ["~/.kube"] } } }`.
- Managed-settings checksum at your gateway (2.1.327+), about 5 minutes: the gateway receives `x-claude-code-managed-settings-checksum`, so you can spot machines whose policy is missing or different. The header's value format isn't documented yet. In `managed-settings.json`: `{ "env": { "CLAUDE_CODE_GATEWAY_HINT_HEADERS": "1" } }`.

## Sources

- [2.1.326 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.326)
- [2.1.327 release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.327)
- [Kubeshark CVE-2026-129236](https://github.com/advisories/GHSA-8vf2-hxg5-crqh)
- [Kubeshark CVE-2026-129235](https://github.com/advisories/GHSA-gj7r-p794-hhq5)
- [code-review-mcp-server CVE-2026-68934](https://github.com/advisories/GHSA-jq3q-62jc-fqq9)
- [MCP Java SDK 2.2.0](https://github.com/modelcontextprotocol/java-sdk/releases/tag/v2.2.0)
- [sandboxing docs (allowWrite)](https://code.claude.com/docs/en/sandboxing)
