# DEVX-029: Pin mcp-server-git and always pass --repository

## Summary

The git README now warns that without '--repository' the server can read and write every repo the user can.

## Details

That flag is its only confinement. PoC: uvx 'mcp-server-git==2026.10.28' with '--repository' set (version pin is the agent's addition).

## Content

### Pin mcp-server-git and always pass `--repository` — Enterprise feasibility: High | Stage: Adopt
- What changed: the [git README](https://github.com/modelcontextprotocol/servers/blob/main/src/git/README.md) now warns that without `--repository` the server can read and write every repo the process can reach. That flag is its only confinement.
- PoC (the README's config shape; the version pin is my addition):
```json
{ "mcpServers": { "git": {
  "command": "uvx",
  "args": ["mcp-server-git==2026.10.28", "--repository", "path/to/git/repo"]
} } }
```
  Then run `uvx --refresh mcp-server-git --help` to refresh the cached copy.
- Success metric: every git MCP entry pins 2026.10.28 or later and passes `--repository`.
- Note: use one entry per repo, and don't give a filesystem MCP server write access to the same tree.
- Sources: [release v2.2.0](https://github.com/modelcontextprotocol/servers/releases/tag/v2.2.0), [PR #5333](https://github.com/modelcontextprotocol/servers/pull/5333), [PyPI 2026.10.28](https://pypi.org/project/mcp-server-git/2026.10.28/) | seen in 3 sources | expires: 2027-01-27

## Sources

- [git README](https://github.com/modelcontextprotocol/servers/blob/main/src/git/README.md)
- [release v2.2.0](https://github.com/modelcontextprotocol/servers/releases/tag/v2.2.0)
- [PR #5333](https://github.com/modelcontextprotocol/servers/pull/5333)
- [PyPI 2026.10.28](https://pypi.org/project/mcp-server-git/2026.10.28/)