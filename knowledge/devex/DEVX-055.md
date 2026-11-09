# DEVX-055: Pin mcp-server-fetch to 2026.11.4 and set --allowed-hosts (MCP reference servers v2.3.0)

## Summary

MCP reference servers v2.3.0 adds an --allowed-hosts flag to mcp-server-fetch: with it set, every request (page, robots.txt, each redirect hop) must match a listed host or is refused. One args change turns the fetch MCP from 'any public host' into an operator allowlist.

## Details

servers v2.3.0 published Nov 4 at 23:28 Israel time; Python packages stamped 2026.11.4 (PR #5392). Without the flag, behaviour is unchanged (still refuses private/loopback/link-local unless --allow-private-ips). Entries are exact hosts, *.domain wildcards (subdomains only, not the apex), or literal IPs. Allowlist and private-address guard are separate: listing localhost still needs --allow-private-ips. Config (from the official fetch README): {"mcpServers": {"fetch": {"command": "uvx", "args": ["mcp-server-fetch", "--allowed-hosts", "docs.python.org", "*.wikipedia.org"]}}}. Pin: uvx mcp-server-fetch==2026.11.4.

## Sources

- [servers v2.3.0](https://github.com/modelcontextprotocol/servers/releases/tag/v2.3.0)
- [PR #5392](https://github.com/modelcontextprotocol/servers/pull/5392)
- [fetch README](https://raw.githubusercontent.com/modelcontextprotocol/servers/main/src/fetch/README.md)
- [PyPI 2026.11.4](https://pypi.org/project/mcp-server-fetch/2026.11.4)
