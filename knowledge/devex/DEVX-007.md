# DEVX-007: Lock down HTTP MCP servers

## Summary

Four CVEs share one pattern: an MCP endpoint reachable without credentials (argocd-mcp, JeecgBoot and others).

## Details

How it works: use stdio for local servers. Any HTTP server should bind to 127.0.0.1 and require a token.

## Content

## 3. Lock down HTTP MCP servers (Feasibility: High, Stage: Adopt)
- **What changed:** four CVEs share one pattern, an MCP endpoint reachable without credentials:
  - argocd-mcp CVE-2026-82456, CVSS 10, fixed in 0.9.0
  - PraisonAI CVE-2026-61427
  - Next.js dev-server MCP CVE-2026-94486, fixed in 16.3.8
  - JeecgBoot CVE-2026-108671
- **How it works:** use stdio for local servers. Any HTTP server should bind to 127.0.0.1 and require a token. On top of that, a managed allowlist controls which servers developers can connect to at all.
- **Effort:** ~15 min.
- **PoC:** first find listeners open on all interfaces with `ss -ltnp | grep -E '0\.0\.0\.0|\[::\]'`. Then set `{"allowManagedMcpServersOnly": true, "allowedMcpServers": [{"serverUrl": "https://mcp.internal.example.com/*"}]}`.
- **Success metric:** no MCP servers listening on 0.0.0.0 across the fleet.
- **Org challenge:** once you add one allow entry, every server must match the list, so take an inventory first.
- **Sources (5):** [Apiiro writeup](https://apiiro.com/blog/cve-2026-82456-argo-cd-mcp-server-kubernetes-takeover/), [GHSA-p2x5-x87w-v2xj](https://github.com/advisories/GHSA-p2x5-x87w-v2xj), [managed MCP docs](https://code.claude.com/docs/en/managed-mcp)

## Sources

- [Apiiro writeup](https://apiiro.com/blog/cve-2026-82456-argo-cd-mcp-server-kubernetes-takeover/)
- [GHSA-p2x5-x87w-v2xj](https://github.com/advisories/GHSA-p2x5-x87w-v2xj)
- [managed MCP docs](https://code.claude.com/docs/en/managed-mcp)