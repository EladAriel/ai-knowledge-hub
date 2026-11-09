# PIPE-003: Pipeline: permission-aware retrieval (ACL)

## Summary

Source ACLs + identity crawl -> ACL fields on every chunk -> identity at query time -> pre/post-filter -> only ….

## Details

Mirror source permissions, never invent them; enforce on search, answers, citations, agents, MCP. Use stable IDs (Entra GUIDs) and the caller's token; no token = no protected docs. ….

## Sources

- [OpenFGA RAG guide](https://openfga.dev/docs/modeling/agents/rag-authorization)
- [Azure query-time ACL](https://learn.microsoft.com/en-us/azure/search/search-query-access-control-rbac-enforcement)
