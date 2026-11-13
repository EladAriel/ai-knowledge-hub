# DEVX-073: Upgrade MCP filesystem/git/fetch servers (reference servers v2.4.0, six advisories) and pin versions by hand

## Summary

MCP reference servers v2.4.0 fix six advisories. Worst: in mcp-server-git a read-only call like git_status on an untrusted repo could run a program named in that repo's .git/config (core.fsmonitor, hooks, filters) with the server's permissions. Fixed: server-filesystem 2.3.0, mcp-server-git / mcp-server-fetch 2026.11.11.

## Details

- Other advisories: symlink-swap races in filesystem reads and move_file; two fetch bypasses (IPv6 fec0::/10 treated as public, path tricks past robots.txt).
- Watch out: npm ranks server-filesystem 2.3.0 below the old date versions (2025.x/2026.x), so it won't be offered as an upgrade. Pin it: `npm install @modelcontextprotocol/server-filesystem@2.3.0`; `uvx mcp-server-git@2026.11.11 --help && uvx mcp-server-fetch@2026.11.11 --help`.
- If .mcp.json runs `npx -y @modelcontextprotocol/server-filesystem` or `uvx mcp-server-git` without a version, add `@2.3.0` or `@2026.11.11`.
- On Windows the filesystem race is narrowed but not closed, and git still doesn't cover directory junctions.
- Related: DEVX-029 (pin mcp-server-git, always pass --repository) and DEVX-055 (mcp-server-fetch --allowed-hosts, v2.3.0). A related guard: make a pre-launch check fail when an MCP server in .mcp.json or the global config runs unpinned (npx/uvx with no version) or below the fixed-version floor. Effort ~20 min.

## Content

**Release notes, Wed Nov 11** (Since yesterday: the MCP reference servers shipped v2.4.0 with security fixes. Claude Code is still at 2.1.322 latest and 2.1.311 stable. Nothing new from Cursor, the MCP Inspector or Aider.)

**Breaking-change alerts**
- **Upgrade the MCP filesystem, git and fetch servers today.** [servers v2.4.0](https://github.com/modelcontextprotocol/servers/releases/tag/v2.4.0) fixes six advisories. The worst is in `mcp-server-git`: until now, a read-only call like `git_status` on an untrusted repo could run a program named in that repo's `.git/config` (`core.fsmonitor`, hooks, filters) with the server's permissions ([GHSA-6hqx-gqrx-c5r2](https://github.com/modelcontextprotocol/servers/security/advisories/GHSA-6hqx-gqrx-c5r2)). The others: symlink-swap races in filesystem reads and `move_file`, and two bypasses in fetch (IPv6 `fec0::/10` was treated as a public address, and some path tricks got past robots.txt). Fixed versions are `server-filesystem` 2.3.0 and `mcp-server-git`/`mcp-server-fetch` 2026.11.11. **Watch out:** npm ranks 2.3.0 *below* the old date versions (2025.x/2026.x), so it won't offer it as an upgrade. Pin it yourself:
  ```bash
  npm install @modelcontextprotocol/server-filesystem@2.3.0
  uvx mcp-server-git@2026.11.11 --help && uvx mcp-server-fetch@2026.11.11 --help
  ```
  If you run `npx -y @modelcontextprotocol/server-filesystem` or `uvx mcp-server-git` without a version in `.mcp.json`, add `@2.3.0` or `@2026.11.11`. On Windows, the filesystem race is narrowed but not closed, and git still doesn't cover directory junctions.

## Sources

- [servers v2.4.0](https://github.com/modelcontextprotocol/servers/releases/tag/v2.4.0)
- [GHSA-6hqx-gqrx-c5r2](https://github.com/modelcontextprotocol/servers/security/advisories/GHSA-6hqx-gqrx-c5r2)
