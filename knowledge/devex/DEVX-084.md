# DEVX-084: Upgrade MCP Inspector to 2.15.0 (or 1.0.5) for four advisories; patch IBM ContextForge MCP Gateway (CVE-2026-110278)

## Summary

MCP Inspector 2.15.0 (Nov 12) and 1.0.5 (Nov 11) fix four advisories: fetch guard now blocks cloud metadata addresses outside 169.254.0.0/16, unbounded POST SSE responses can no longer crash the proxy, the server.json preview shows every env value and flags NODE_OPTIONS / npm_config_registry, and mcpdo checks the daemon is real before sending credentials. Separately, IBM ContextForge MCP Gateway CVE-2026-110278 (CVSS 7.4) ignores the per-server identity-propagation switch on tool calls; fixed in v1.1.1.

## Details

- Upgrade: `npx @modelcontextprotocol/inspector@latest` (or `@v1-latest`). Advisories: GHSA-fvg8-f358-w2c8 (the only fix in 1.0.5), GHSA-9w48-x22j-rrm7, GHSA-pp85-586h-2m95, GHSA-5572-x678-xmv8.
- ContextForge: upgrade to v1.1.1; if you can't yet, set `IDENTITY_PROPAGATION_ENABLED=false`. Related medium bug CVE-2026-110195 lets cached upstream tokens be reused across credentials.
- Related: DEVX-054 (MCP Inspector 2.14.0 / 1.0.4 advisories).

## Content

Context (Nov 15): Claude Code shipped 2.1.323 and 2.1.325 since Thursday; latest is now 2.1.325, stable is still 2.1.311. The MCP Inspector's 2.15.0 security release had been missed in the Thursday check. Nothing new from the MCP servers, SDKs, Aider or Cursor.

- **MCP Inspector 2.15.0 and 1.0.5 fix four advisories (missed on Thursday).** They came out Nov 12 at 02:46 Israel time (2.15.0) and Nov 11 at 23:39 (1.0.5) ([2.15.0](https://github.com/modelcontextprotocol/inspector/releases/tag/2.15.0), [1.0.5](https://github.com/modelcontextprotocol/inspector/releases/tag/1.0.5)). The fixes:
  - The fetch guard now blocks cloud metadata addresses outside `169.254.0.0/16`, such as `100.100.100.200` ([GHSA-fvg8-f358-w2c8](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-fvg8-f358-w2c8), the only fix in 1.0.5).
  - A server streaming an unbounded POST SSE response can no longer crash the proxy ([GHSA-9w48-x22j-rrm7](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-9w48-x22j-rrm7)).
  - The `server.json` preview now shows every env value and flags `NODE_OPTIONS` and `npm_config_registry` ([GHSA-pp85-586h-2m95](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-pp85-586h-2m95)).
  - `mcpdo` now checks that the daemon is real before it sends credentials ([GHSA-5572-x678-xmv8](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-5572-x678-xmv8)).
  - Upgrade with `npx @modelcontextprotocol/inspector@latest` (or `@v1-latest`).
- **If you run IBM ContextForge MCP Gateway:** [CVE-2026-110278](https://github.com/advisories/GHSA-774m-v6g3-r639) (CVSS 7.4) means the per-server identity-propagation switch is ignored on tool calls, so user identity can reach upstream MCP servers that were set not to get it. It's fixed in v1.1.1 ([IBM bulletin](https://www.ibm.com/support/pages/node/7296489)). If you can't upgrade yet, set `IDENTITY_PROPAGATION_ENABLED=false`. A related medium bug, [CVE-2026-110195](https://github.com/advisories/GHSA-cvpg-9259-jm3r), lets cached upstream tokens be reused across credentials.

## Sources

- [Inspector 2.15.0](https://github.com/modelcontextprotocol/inspector/releases/tag/2.15.0)
- [Inspector 1.0.5](https://github.com/modelcontextprotocol/inspector/releases/tag/1.0.5)
- [GHSA-fvg8-f358-w2c8](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-fvg8-f358-w2c8)
- [GHSA-9w48-x22j-rrm7](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-9w48-x22j-rrm7)
- [GHSA-pp85-586h-2m95](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-pp85-586h-2m95)
- [GHSA-5572-x678-xmv8](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-5572-x678-xmv8)
- [CVE-2026-110278](https://github.com/advisories/GHSA-774m-v6g3-r639)
- [IBM bulletin](https://www.ibm.com/support/pages/node/7296489)
- [CVE-2026-110195](https://github.com/advisories/GHSA-cvpg-9259-jm3r)
