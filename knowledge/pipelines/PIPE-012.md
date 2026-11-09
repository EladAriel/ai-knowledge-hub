# PIPE-012: Pipeline: permissions and ACLs (fail-closed)

## Summary

verified token -> groups lookup (deny on failure) -> permission engine returns allowed IDs/filter -> filtered hybrid ….

## Details

Sync permissions separately and watch defaults (Elastic DLS: doc without ACL field is public). Pick filtering by how many docs a user sees (OpenFGA: search-then-check / list-then-search up to ~1,000 docs / local copy + recheck); ….

## Sources

- [OpenFGA search with …](https://openfga.dev/docs/interacting/search-with-permissions)
- [Cerbos Query Plan](https://docs.cerbos.dev/cerbos/latest/recipes/ai/rag-authorization/)
- [MCP authorization spec](https://modelcontextprotocol.io/specification/draft/basic/authorization)
- [promptfoo cross-session-leak](https://www.promptfoo.dev/docs/red-team/plugins/cross-session-leak/)
