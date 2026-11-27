# DEVX-100: Run local MCP servers over stdio, not localhost HTTP (Jupyter MCP critical CVE-2026-77359, k8s-mcp-server CVE-2026-130007)

## Summary

More advisories of the same kind this week: a web page you visit can drive a local MCP server that listens over HTTP. Examples: Jupyter MCP (critical CVE-2026-77359, fixed in 1.0.3) and k8s-mcp-server (CVE-2026-130007, no auth by default, fixed in 1.1.0). Use stdio wherever the server offers it, and upgrade the rest. A single command shows which tools any browser tab could reach. Seen in 4+ advisories. Enterprise feasibility: High. Stage: Adopt. Effort: ~10 min.

## Details

- Find HTTP-configured MCP servers:

```bash
grep -n '"url"' ~/.cursor/mcp.json .cursor/mcp.json .mcp.json 2>/dev/null; claude mcp list
```

- Switch to stdio where offered; upgrade Jupyter MCP to 1.0.3+ and k8s-mcp-server to 1.1.0+.
- Tip for unattended runs: fail the run if a local MCP server is configured with a localhost URL instead of stdio, unless it is on an explicit exception list.
- Reported Nov 22. Expires Feb 20, 2027.
- Related: DEVX-007 (lock down HTTP MCP servers), DEVX-095 (Supergateway API key, the same browser-drives-local-MCP class).

## Content

### Run local MCP servers over stdio, not localhost HTTP — Enterprise feasibility: High | Stage: Adopt

- **Problem → fix:** this week brought more advisories of the same kind: a web page you visit can drive a local MCP server that listens over HTTP. Examples are Jupyter MCP (critical CVE-2026-77359, fixed in 1.0.3) and k8s-mcp-server (CVE-2026-130007, no auth by default, fixed in 1.1.0). Use stdio wherever the server offers it, and upgrade the rest.
- **Why it matters:** a single command shows which tools any browser tab could reach. Seen in 4+ advisories.
- **Effort:** ~10 min.

```bash
grep -n '"url"' ~/.cursor/mcp.json .cursor/mcp.json .mcp.json 2>/dev/null; claude mcp list
```

Advisories: [Jupyter MCP](https://github.com/advisories/GHSA-9x8x-crjq-g64h) · [k8s-mcp-server](https://github.com/advisories/GHSA-m932-63jc-4jqq) | expires: 2027-02-20

## Sources

- [Jupyter MCP advisory](https://github.com/advisories/GHSA-9x8x-crjq-g64h)
- [k8s-mcp-server advisory](https://github.com/advisories/GHSA-m932-63jc-4jqq)
