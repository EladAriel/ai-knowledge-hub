# PIPE-012: Pipeline: permissions and ACLs (fail-closed)

## Summary

verified token -> groups lookup (deny on failure) -> permission engine returns allowed IDs/filter -> filtered hybrid search -> live recheck of top hits -> rerank -> LLM -> answer inherits strictest sensitivity label -> per-permission-set cache/memory -> audit.

## Details

Sync permissions separately and watch defaults (Elastic DLS: doc without ACL field is public). Pick filtering by how many docs a user sees (OpenFGA: search-then-check / list-then-search up to ~1,000 docs / local copy + recheck); Cerbos Query Plan turns policy into a vector-store filter. Never fall back to unfiltered search. Agents need tokens issued for them; no token passthrough (MCP authorization spec); token exchange limits to what both user and agent may access. Eval: 3 users + 10 canary docs (+ promptfoo cross-session-leak plugin) in under a day.

## Content

## Pipeline pattern of the day: permissions and ACLs

verified user token -> look up the user's groups (deny if this fails) -> permission engine returns allowed IDs or a filter -> hybrid search with that filter applied first -> live recheck of the top hits -> rerank -> LLM -> answer inherits the sources' sensitivity labels, and citations are checked -> cache and memory kept separate per permission set -> audit log

- **Sync permissions separately from content, and watch the defaults.** In [Elastic document-level security](https://www.elastic.co/docs/reference/search-connectors/es-dls-overview), a document with no ACL field is visible to everyone, so turn the feature on before the first content sync.
- **Pick the filtering approach by how many docs a user can see.** [OpenFGA lays out three options](https://openfga.dev/docs/interacting/search-with-permissions):
  - Search first, then check each result.
  - List the allowed docs first, then search only those. This works up to about 1,000 docs.
  - Keep a local copy of permissions, then recheck results to catch recent revocations.

  [Cerbos Query Plan](https://docs.cerbos.dev/cerbos/latest/recipes/ai/rag-authorization/) turns a permission policy into a filter your vector store understands.
- **Never fall back to an unfiltered search.** If the live check fails, drop the result ([WorkOS on three ways to enforce access](https://workos.com/blog/rag-access-control-document-permissions)).
- **Agents acting for a user need tokens meant for them.** An MCP server must only accept tokens issued for that server, and must not forward them anywhere else ([MCP authorization spec](https://modelcontextprotocol.io/specification/draft/basic/authorization)). With token exchange, the agent can only reach what both the user and the agent are allowed to.
- **Generated content inherits sensitivity.**
  - Microsoft 365 Copilot's answers take the strictest sensitivity label among their sources

   promptfoo's [cross-session-leak plugin](https://www.promptfoo.dev/docs/red-team/plugins/cross-session-leak/) covers the social-engineering side.

A first version with 3 users and 10 canary docs takes under a day.

**What it catches:** filters that fail open, retrieval running under a broad service account, permission syncs that have gone stale, cache or memory leaking between users, and summaries that ignore permissions.

**Who runs it:** Devs run it in CI. Architects own the list of fake users and planted docs. Product reviews the recall side, so security doesn't quietly make answers worse.

## Sources

- [OpenFGA lays out three options](https://openfga.dev/docs/interacting/search-with-permissions)
- [Cerbos Query Plan](https://docs.cerbos.dev/cerbos/latest/recipes/ai/rag-authorization/)
- [MCP authorization spec](https://modelcontextprotocol.io/specification/draft/basic/authorization)
- [promptfoo cross-session-leak](https://www.promptfoo.dev/docs/red-team/plugins/cross-session-leak/)
- [Elastic document-level security](https://www.elastic.co/docs/reference/search-connectors/es-dls-overview)
- [WorkOS on three ways to enforce access](https://workos.com/blog/rag-access-control-document-permissions)
- Microsoft 365 Copilot's answers take the strictest sensitivity label among their sources
