# DEVX-029: Pin mcp-server-git and always pass --repository

## Summary

The git README now warns that without '--repository' the server can read and write every repo the user can.

## Details

That flag is its only confinement.

## Sources

- [git README](https://github.com/modelcontextprotocol/servers/blob/main/src/git/README.md)
- [release v2.2.0](https://github.com/modelcontextprotocol/servers/releases/tag/v2.2.0)
- [PR #5333](https://github.com/modelcontextprotocol/servers/pull/5333)
- [PyPI 2026.10.28](https://pypi.org/project/mcp-server-git/2026.10.28/)
