# METH-148: New terms (Nov 13, enterprise knowledge): geometric access control, preserve at write / resolve at read, overfetch, LookupResources, deny-wins, RLS

## Summary

One-line terms (Nov 13) on the permissions and access control stage.

## Details

Geometric access control: transforming embeddings per access policy so only vectors from the same policy match. Policy-membership hiding: not revealing which access group a document belongs to. Preserve at write, resolve at read: never merge or delete when saving, and decide at query time instead. Bi-temporal provenance graph: stores each fact with when it was true, when it was recorded, and its source. Resource selection: picking which source, like Slack, Jira or email, to search first. Overfetch multiplier: fetching extra candidates so enough are left after the permission filter. LookupResources and CheckBulkPermissions: SpiceDB calls that list everything a user can see, or check many items at once. Deny-wins: an explicit deny beats any allow. Row-level security: the database itself filters rows for each user or customer. Query-routed context: building the context differently depending on what the question needs. Recurring themes: do the permission check outside the model (the eighth time this theme came up, now including embeddings); keeping raw conversations beats keeping only summaries for memory (MAPE, after Nov 4); vendors keep shipping governed business definitions for agents (Databricks and Neo4j).

## Sources

- No single link was recorded for this terms list. Related public sources (see PIPE-030, METH-144, METH-145, METH-146):
- [Isolation Is Not Confidentiality](https://arxiv.org/abs/2611.14061)
- [DISCERN](https://arxiv.org/abs/2611.15729)
- [Wayfinder](https://arxiv.org/abs/2611.16053)
- [Elastic: RAG with SpiceDB](https://www.elastic.co/search-labs/blog/fine-grained-authorization-elasticsearch-rag-spicedb)
- [Authorization-First Retrieval](https://aclanthology.org/2026.trustnlp-main.15/)
