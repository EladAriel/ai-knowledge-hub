# DEVX-007: Lock down HTTP MCP servers

## Summary

Four CVEs share one pattern: an MCP endpoint reachable without credentials (argocd-mcp, JeecgBoot and others).

## Details

How it works: use stdio for local servers. Any HTTP server should bind to 127.0.0.1 and require a token. ….

## Sources

- [Apiiro writeup](https://apiiro.com/blog/cve-2026-82456-argo-cd-mcp-server-kubernetes-takeover/)
- [GHSA-p2x5-x87w-v2xj](https://github.com/advisories/GHSA-p2x5-x87w-v2xj)
- [managed MCP docs](https://code.claude.com/docs/en/managed-mcp)
