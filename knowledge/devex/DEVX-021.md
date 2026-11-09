# DEVX-021: Treat remote MCP servers as hostile to the client, too

## Summary

Three cases in one week where connecting to an MCP server compromises the host.

## Details

One is the FastMCP client RCE. Another is an opencode RCE on Windows and WSL through a server's OAuth URL, fixed quietly in 1.18.33 with no CVE (Pillar Security).

## Content

## 3. Treat remote MCP servers as hostile to the client, too: Enterprise feasibility High | Stage Adopt
- **What changed:** this week brought three cases where connecting to an MCP server compromises the host. One is the FastMCP client RCE (the alert above). Another is an opencode RCE on Windows and WSL through a server's OAuth URL, fixed quietly in 1.18.33 with no CVE ([Pillar Security](https://www.pillar.security/blog/open-and-shut-remote-code-execution-in-opencode-via-mcp-oauth)). The third is Langflow's MCP config RCE, which is now being exploited in the wild ([The Hacker News](https://thehackernews.com/2026/10/langflows-critical-authenticated-rce.html)).
- **How it works:** set minimum versions in lockfiles and check them by package version, since scanners that match on CVE IDs miss two of the three. Your `allowedMcpServers` allowlist stays the policy layer.
- **Effort:** ~20 min.
- **PoC:**
```bash
# requirements: fastmcp>=3.4.9,<4   (or fastmcp>=4.1.1; 2.x has no fix)
pip show fastmcp langflow 2>/dev/null | rg '^(Name|Version)'   # langflow >= 1.10.3, LANGFLOW_AUTO_LOGIN=false
npm ls -g opencode-ai                                          # >= 1.18.33 on Windows/WSL
```
- **Success metric:** within 72h, every lockfile and dev machine is at or above those versions.
- **Sources:** [FastMCP advisories](https://github.com/PrefectHQ/fastmcp/security/advisories), [Pillar Security](https://www.pillar.security/blog/open-and-shut-remote-code-execution-in-opencode-via-mcp-oauth), [Langflow GHSA-w794](https://github.com/langflow-ai/langflow/security/advisories/GHSA-w794-rj3p-xv45), [The Hacker News](https://thehackernews.com/2026/10/langflows-critical-authenticated-rce.html) (seen in 6 sources)

## Sources

- [Pillar Security](https://www.pillar.security/blog/open-and-shut-remote-code-execution-in-opencode-via-mcp-oauth)
- [The Hacker News](https://thehackernews.com/2026/10/langflows-critical-authenticated-rce.html)
- [FastMCP advisories](https://github.com/PrefectHQ/fastmcp/security/advisories)
- [Langflow GHSA-w794](https://github.com/langflow-ai/langflow/security/advisories/GHSA-w794-rj3p-xv45)