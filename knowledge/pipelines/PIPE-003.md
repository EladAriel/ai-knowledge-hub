# PIPE-003: Pipeline: permission-aware retrieval (ACL)

## Summary

Source ACLs + identity crawl -> ACL fields on every chunk -> identity at query time -> pre/post-filter -> only authorized chunks reach the LLM -> re-check at action time + audit.

## Details

Mirror source permissions, never invent them; enforce on search, answers, citations, agents, MCP. Use stable IDs (Entra GUIDs) and the caller's token; no token = no protected docs. Pre-filter (ListObjects/LookupResources -> metadata filter) when users see a small slice; post-filter (BatchCheck, over-fetch 2-3x) when they see most. Enforce on the server for tool results and multi-turn context; gate cached/derived results by lineage. Devs: wrap the retriever with OpenFGA/SpiceDB authorization; negative ACL tests in CI.

## Content

## Pipeline pattern of the day: permissions/ACL (permission-aware retrieval)

`Source ACLs + identity crawl (users, groups, memberships)` -> `attach ACL fields to every chunk at ingest` -> `map the user's identity at query time (token -> user + group IDs)` -> `pre-filter (authorized IDs into the vector/keyword search) OR post-filter (over-fetch, then batch-check)` -> `only authorized chunks reach the LLM and citations` -> `re-check at click and action time + audit log`

- **Mirror the source's permissions. Never invent them.** Ingest ACLs, groups, and memberships with the content. Enforce on every surface: search, AI answers, citations, agents, and MCP ([Glean security principles](https://docs.glean.com/security/security-principles)). Index identities before the docs that reference them. A group with no members is an error ([Glean Indexing SDK](https://developers.glean.com/libraries/indexing-sdk/permissions)).
- **Use stable IDs and pass the user's token.** Azure AI Search stores Entra object IDs (GUIDs, not emails) in `userIds`/`groupIds` fields and trims results using the caller's token. With no token, ACL-protected docs are not returned. ACL changes only apply after the next sync ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/search-query-access-control-rbac-enforcement)).
- **Pick pre- or post-filter by how much each user can access.** Pre-filter (ListObjects / LookupResources, then pass IDs as a metadata filter) when users see a small slice. Post-filter (BatchCheck) when they see most docs, and over-fetch 2–3x top-k ([OpenFGA RAG guide](https://openfga.dev/docs/modeling/agents/rag-authorization), [SpiceDB RAG post](https://authzed.com/blog/fine-grained-authorization-using-spicedb-for-retrieval-augmented-generation-rag)). Research on policy-aware vector search: [arXiv 2606.19803](https://arxiv.org/abs/2606.19803).
- **Enforce on the server, including for tools and multi-turn context.** Tool results and context built up across turns also leak. ABAC (attribute-based access control) gating on the server removed cross-tenant leakage in [arXiv 2605.05287](https://arxiv.org/abs/2605.05287).
- **Gate derived and cached results too.** A cached answer or KPI computed from a column the user cannot see is still a leak. Record lineage (what data a result came from) and serve the cached result only if the user can access every input ([arXiv 2610.07258](https://arxiv.org/abs/2610.07258), proof of concept only).
- **Who owns it:**
  - *Architects:* own the identity mapping (source accounts to your IdP) and the ACL schema on every chunk. Set the pre/post-filter policy and the sync freshness target (SLA).
  - *Product:* decide which sources are "live/federated" (always fresh) vs indexed (cheaper but stale). Make "0 leaks" a launch gate, and explain to users why an answer can differ from person to person.
  - *Devs:* wrap the retriever with an authorization step (e.g. a LangChain custom retriever or LlamaIndex postprocessor calling OpenFGA/SpiceDB). Add negative ACL tests to CI.

## Sources

- [OpenFGA RAG guide](https://openfga.dev/docs/modeling/agents/rag-authorization)
- [Azure query-time ACL](https://learn.microsoft.com/en-us/azure/search/search-query-access-control-rbac-enforcement)
- [Glean security principles](https://docs.glean.com/security/security-principles)
- [Glean Indexing SDK](https://developers.glean.com/libraries/indexing-sdk/permissions)
- [SpiceDB RAG post](https://authzed.com/blog/fine-grained-authorization-using-spicedb-for-retrieval-augmented-generation-rag)
- [arXiv 2606.19803](https://arxiv.org/abs/2606.19803)
- [arXiv 2605.05287](https://arxiv.org/abs/2605.05287)
- [arXiv 2610.07258](https://arxiv.org/abs/2610.07258)