# DEVX-055: Pin mcp-server-fetch to 2026.11.4 and set --allowed-hosts (MCP reference servers v2.3.0)

## Summary

MCP reference servers v2.3.0 adds an --allowed-hosts flag to mcp-server-fetch: with it set, every request (page, robots.txt, each redirect hop) must match a listed host or is refused. One args change turns the fetch MCP from 'any public host' into an operator allowlist.

## Details

servers v2.3.0 published Nov 4 at 23:28 Israel time; Python packages stamped 2026.11.4 (PR #5392). Without the flag, behaviour is unchanged (still refuses private/loopback/link-local unless --allow-private-ips). Entries are exact hosts, *.domain wildcards (subdomains only, not the apex), or literal IPs. Allowlist and private-address guard are separate: listing localhost still needs --allow-private-ips. Config (from the official fetch README): {"mcpServers": {"fetch": {"command": "uvx", "args": ["mcp-server-fetch", "--allowed-hosts", "docs.python.org", "*.wikipedia.org"]}}}. Pin: uvx mcp-server-fetch==2026.11.4. Success metric: org fetch configs name an explicit allowlist; a request to an unlisted host returns an error naming the refused host. Org challenge: teams relying on open-web fetch for research need a maintained host list (or a separate unrestricted profile on sandboxed research machines). The same release ships filesystem 2.2.0 (append_file, copy_file, tool annotations), memory 2.1.0, sequential-thinking 2.1.1, everything 2.2.1 (feature work, not advisories). Also listed as a ready-to-use mod (~10 min). Enterprise feasibility High, stage Adopt, seen in 3 sources.

## Content

**[Pin mcp-server-fetch to 2026.11.4 (MCP reference servers v2.3.0) and set --allowed-hosts so the fetch MCP cannot call arbitrary public hosts](https://github.com/modelcontextprotocol/servers/releases/tag/v2.3.0)**
- **urls_extra:** ["https://github.com/modelcontextprotocol/servers/pull/5392", "https://raw.githubusercontent.com/modelcontextprotocol/servers/main/src/fetch/README.md", "https://pypi.org/project/mcp-server-fetch/2026.11.4/"]
- **what_changed:** servers v2.3.0 published Nov 4 at 21:28Z (23:28 Israel time). Python packages stamped 2026.11.4 (PyPI upload ~21:34Z). New operator flag on mcp-server-fetch: --allowed-hosts HOST [HOST ...] (PR #5392). With it set, every request the server sends (tool page, prompt page, robots.txt, every redirect hop) must name a listed host or is refused before send. Without the flag, behaviour is unchanged (still refuses private/loopback/link-local unless --allow-private-ips). Also ships filesystem 2.2.0 (append_file, copy_file, tool annotations), memory 2.1.0, sequential-thinking 2.1.1, everything 2.2.1 — feature work, not security advisories.
- **how_it_works:** Add the flag to the MCP server args allowlist in Claude Code / Cursor mcp config. Entries are exact hosts, *.domain wildcards (subdomains only, not the apex), or literal IPs. Allowlist and private-address guard are separate: listing localhost still needs --allow-private-ips.
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 15
- **poc_snippet:** # from the official fetch README (Customization - Allowed hosts)
{
  "mcpServers": {
    "fetch": {
      "command": "uvx",
      "args": ["mcp-server-fetch", "--allowed-hosts", "docs.python.org", "*.wikipedia.org"]
    }
  }
}
# pin: uvx mcp-server-fetch==2026.11.4 ...   or pip show mcp-server-fetch
- **success_metric:** Fetch MCP configs in the org name an explicit --allowed-hosts list; a request to an unlisted host returns an error naming the refused host.
- **org_challenge_if_relevant:** Teams that rely on open-web fetch for research will need a maintained host list (or a separate unrestricted profile for sandboxed research machines).
- **project_health_if_relevant:** Official MCP reference-servers release; README documents the flag.
- **source_count:** 3
- **benefit_to_effort:** High
- **why_enterprise_simple:** One args-list change turns the reference fetch server from 'any public host' into an operator allowlist, with no custom code.

**[mcp-server-fetch --allowed-hosts operator allowlist (from reference servers v2.3.0 README)](https://raw.githubusercontent.com/modelcontextprotocol/servers/main/src/fetch/README.md)**
- **what_it_gives:** Restricts the official fetch MCP to named hosts (exact, *.subdomain, or literal IP). Checked before every request including robots.txt and redirect hops. Combine with the private-address guard (default on).
- **effort_minutes:** 10
- **snippet:** {
  "mcpServers": {
    "fetch": {
      "command": "uvx",
      "args": ["mcp-server-fetch", "--allowed-hosts", "docs.python.org", "*.wikipedia.org"]
    }
  }
}
- **source_credit:** modelcontextprotocol/servers src/fetch/README.md 'Customization - Allowed hosts' (JSON example copied verbatim)

## Sources

- [servers v2.3.0](https://github.com/modelcontextprotocol/servers/releases/tag/v2.3.0)
- [PR #5392](https://github.com/modelcontextprotocol/servers/pull/5392)
- [fetch README](https://raw.githubusercontent.com/modelcontextprotocol/servers/main/src/fetch/README.md)
- [PyPI 2026.11.4](https://pypi.org/project/mcp-server-fetch/2026.11.4)