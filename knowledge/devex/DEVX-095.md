# DEVX-095: Put an API key on Supergateway (two unpatched high CVEs: any web page can drive your MCP tools in WebSocket mode)

## Summary

Supergateway has two unpatched high CVEs (CVE-2026-132121, CVE-2026-131857). In WebSocket mode, any web page can drive your tools. There is no patched release yet (npm latest is still 4.2.2). Make the gateway require a key and serve Streamable HTTP instead of WebSocket/SSE. Enterprise feasibility: High. Stage: Adopt. Effort: ~10 min.

## Details

- PoC:

```
npx -y supergateway --stdio "<your server cmd>" --outputTransport streamableHttp --apiKey "$MCP_API_KEY"
```

- Why it matters: "any browser tab can call my MCP tools" becomes "only callers with the key can," starting today.
- Seen in 3 sources. Expires Feb 17, 2027.

## Content

- **Supergateway has two unpatched high CVEs** (CVE-2026-132121, CVE-2026-131857), as of Nov 19. In WebSocket mode, any web page can drive your tools.

### 2. Put an API key on Supergateway — Enterprise feasibility: High | Stage: Adopt

- **Problem → fix:** there is no patched release yet (npm latest is still 4.2.2). Make the gateway require a key and serve Streamable HTTP instead of WebSocket/SSE.
- **Why it matters:** "any browser tab can call my MCP tools" becomes "only callers with the key can," starting today.
- **Effort:** ~10 min

```
npx -y supergateway --stdio "<your server cmd>" --outputTransport streamableHttp --apiKey "$MCP_API_KEY"
```

[README: Requiring an API key](https://github.com/supercorp-ai/supergateway#requiring-an-api-key) | 3 sources | expires: 2027-02-17

## Sources

- [Supergateway README: Requiring an API key](https://github.com/supercorp-ai/supergateway#requiring-an-api-key)
- [CVE-2026-132121](https://github.com/advisories/GHSA-cp8r-6jmm-c5qw)
