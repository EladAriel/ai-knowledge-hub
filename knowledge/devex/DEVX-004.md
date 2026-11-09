# DEVX-004: Diff to the MCP server interface before upgrading

## Summary

The official repo of MCP servers adopted in CI a comparison of tools, prompts, resources and capabilities between versions.

## Content

### 4. Diff for the MCP server interface before upgrading — Feasibility for the enterprise: medium Stage: Trial
- **The essence of the change:** The official repo of MCP servers adopted in CI a comparison of tools, prompts, resources and capabilities between versions. An organization can use the same test to detect a rug-pull or a silent change in tool descriptions before approving an upgrade.
- **Technical mechanism:** The CLI `mcp-server-diff` (version 3.0.0, MIT).
- **Practical step (PoC):**
```bash
npx mcp-server-diff -b "npx -y @modelcontextprotocol/server-filesystem@<PINNED> /tmp" \
  -t "npx -y @modelcontextprotocol/server-filesystem@latest /tmp" -o markdown
```
- **Measure of success:** Every MCP upgrade comes with a PR approved diff.
- **Effort:** ~15 minutes
- **Sources:** [PR #4975](https://github.com/modelcontextprotocol/servers/pull/4975), [mcp-server-diff](https://github.com/SamMorrowDrums/mcp-server-diff) | Appears in 2 sources Expiration: 2027-01-08

---

## Sources

- [PR #4975](https://github.com/modelcontextprotocol/servers/pull/4975)
- [mcp-server-diff](https://github.com/SamMorrowDrums/mcp-server-diff)
