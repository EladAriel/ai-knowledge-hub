# PIPE-021: Pipeline: permissions for derived knowledge and agent identity

## Summary

sync permissions from source -> chunks inherit doc ACL + sensitivity label -> summaries, graph nodes, memories and caches get only the access shared by all their sources -> query runs as the user, not the agent -> permission filter in the index -> live recheck of top results at the source -> redact sensitive fields -> audit log.

## Details

Search as the user, not the agent: an agent searching as itself returns whatever the agent can see; AWS says its own permission filtering isn't true authorization, the app must verify the user and pass their identity (QueryNow guide). Synced permissions go stale between syncs, so recheck the final top results live at the source (AWS two-step check in Bedrock and Quick). Sensitivity labels travel with content: Azure AI Search checks Purview labels and SharePoint permissions at query time with the user's Microsoft sign-in token. A summary of 5 docs is visible only to people who can see all 5 (ACL intersection): store source_ids on every derived item, recompute access when any source changes, don't index anything you can't trace to its sources.

## Sources

- [QueryNow: permission-aware retrieval](https://www.querynow.com/ai-agents/knowledge/permission-aware-retrieval)
- [Azure AI Search document-level access](https://learn.microsoft.com/en-us/azure/search/search-document-level-access-overview)
