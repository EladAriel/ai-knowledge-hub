# DEVX-094: Pin the patched MCP git and filesystem servers (official MCP servers v2.5.0 fix 8 vulnerabilities, 5 high in mcp-server-git)

## Summary

Official MCP servers v2.5.0 fix 8 vulnerabilities. Five are high and in mcp-server-git: a repo you didn't write can run commands on your machine. Most setups run mcp-server-git unpinned; pin 2026.11.18. The filesystem server's new 2.4.0 is never offered as an upgrade, because npm thinks the old 2025.x/2026.x versions are newer, so install it by name. Enterprise feasibility: High. Stage: Adopt. Effort: ~10 min.

## Details

- PoC:

```
claude mcp add git -- uvx mcp-server-git@2026.11.18 --repository "$PWD"
npm install @modelcontextprotocol/server-filesystem@2.4.0
```

- Why it matters: about 10 minutes closes six of the eight holes and leaves a version you can audit. Until fix #5599 lands, don't let agents merge untrusted branches.
- Seen in 5 sources. Expires Feb 17, 2027.
- Related: DEVX-073 (servers v2.4.0, six advisories, same npm version-ordering trap with filesystem 2.3.0), DEVX-029 (pin mcp-server-git, always pass --repository).
- If you run a gate that fails on unpinned MCP servers: raise its minimum pins to the same git 2026.11.18 and filesystem 2.4.0, also pin mcp-server-fetch 2026.11.18 (internal-address guard), and require Git 2.33 or newer when submodules exist.

## Content

- **Official MCP servers v2.5.0 fix 8 vulnerabilities (Nov 19).** Five are high and in `mcp-server-git`: a repo you didn't write can run commands on your machine. [Release](https://github.com/modelcontextprotocol/servers/releases/tag/v2.5.0)

### 1. Pin the patched MCP git + filesystem servers — Enterprise feasibility: High | Stage: Adopt

- **Problem → fix:** most setups run `mcp-server-git` unpinned. Pin 2026.11.18. The filesystem server's new 2.4.0 is never offered as an upgrade, because npm thinks the old 2025.x/2026.x versions are newer, so install it by name.
- **Why it matters:** about 10 minutes closes six of the eight holes and leaves a version you can audit. Until fix #5599 lands, don't let agents merge untrusted branches.
- **Effort:** ~10 min

```
claude mcp add git -- uvx mcp-server-git@2026.11.18 --repository "$PWD"
npm install @modelcontextprotocol/server-filesystem@2.4.0
```

[v2.5.0 notes](https://github.com/modelcontextprotocol/servers/releases/tag/v2.5.0) | 5 sources | expires: 2027-02-17

## Sources

- [servers v2.5.0 notes](https://github.com/modelcontextprotocol/servers/releases/tag/v2.5.0)
