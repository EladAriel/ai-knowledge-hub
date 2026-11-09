# DEVX-021: Treat remote MCP servers as hostile to the client, too

## Summary

Three cases in one week where connecting to an MCP server compromises the host. Another is an opencode RCE on Windows and WSL through a server's OAuth URL, fixed quietly in 1.18.33 with no CVE (Pillar Security).

## Details

One is the FastMCP client RCE. Another is an opencode RCE on Windows and WSL through a server's OAuth URL, fixed quietly in 1.18.33 with no CVE (Pillar Security). ….

## Sources

- [Pillar Security](https://www.pillar.security/blog/open-and-shut-remote-code-execution-in-opencode-via-mcp-oauth)
- [The Hacker News](https://thehackernews.com/2026/10/langflows-critical-authenticated-rce.html)
- [FastMCP advisories](https://github.com/PrefectHQ/fastmcp/security/advisories)
