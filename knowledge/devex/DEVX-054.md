# DEVX-054: Upgrade MCP Inspector to 2.14.0 (or 1.0.4 on v1): three medium security advisories fixed

## Summary

MCP Inspector 2.14.0 (npm latest) and deprecated 1.0.4 (v1-latest) fix three medium advisories: MCP App sandbox-frame escape (connectDomains was not an egress boundary), unvalidated server.json import and non-http(s) URL elicitations, and an outputSchema.pattern ReDoS. Upgrade before connecting untrusted servers or reviewing MCP Apps.

## Details

Released Nov 5 around 01:55–02:17 Israel time. GHSA-h9j8-vj8g-v3gg (CVSS 6.1): an MCP App can navigate its sandbox frame away while the proxy still relays with targetOrigin '*', so the app's connectDomains CSP was not an egress boundary (v2 only, >=2.0.0 \<=2.13.0). GHSA-rwv7-mh2c-ff2p: server.json import did not validate runtimeArguments / identifier / environment variables, and URL elicitations accepted non-http(s) schemes; import now shows the exact command before save. GHSA-2fw8-7jmw-r937 (CVSS 6.5): a malicious tool outputSchema.pattern can ReDoS-stall the UI; v2 uses a bounded linear-time matcher, v1.0.4 strips patterns. Node engine floor is now ^22.23.4 || ^24.22.1 || >=26.12.1 (EBADENGINE is advisory only).

## Sources

- [Inspector 2.14.0 release](https://github.com/modelcontextprotocol/inspector/releases/tag/2.14.0)
- [GHSA-h9j8](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-h9j8-vj8g-v3gg)
- [GHSA-rwv7](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-rwv7-mh2c-ff2p)
- [GHSA-2fw8](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-2fw8-7jmw-r937)
- [Forkast write-up](https://forkast.news/mcp-inspector-2-14-0-fixes-three-privately-reported-vulnerabilities-and-changes-developer-facing-behavior)
