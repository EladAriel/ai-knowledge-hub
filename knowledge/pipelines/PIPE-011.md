# PIPE-011: Pipeline: indexing with alias switch and rollback

## Summary

chunks + metadata (doc_id, version, acl, embed_model) -> versioned store -> build vector/BM25/graph into a NEW index -> recall audit -> switch alias -> keep old index for rollback.

## Details

Never mix embedding models in one index; store model+version per row; rebuild and switch an index alias. Filtered search trap: pgvector filters after the scan (10% filter with ef_search 40 returns ~4 rows) -> iterative index scans, higher budget, exact scans for small scopes. Index is rebuildable; raw text is source of truth. Refresh stats after bulk loads. halfvec kept recall with a ~1/3 smaller index.

## Content

## Pipeline pattern of the day: indexing

chunks + metadata (doc_id, version, acl, embed_model) -> versioned store -> build vector, keyword (BM25) and graph indexes into a NEW index -> recall audit -> switch the alias to the new index -> keep the old index for rollback

- **Never mix embedding models in one index.** Store the model name and version on every row, rebuild into a new index, and switch an [index alias](https://learn.microsoft.com/en-us/azure/search/search-how-to-alias) so the app keeps querying the same name.
- **Filtered search is a known trap.** In [pgvector](https://github.com/pgvector/pgvector), filters apply after the index scan. A filter that matches 10% of rows, with the default `ef_search` of 40, returns only about 4 rows. Turn on iterative index scans or raise the scan budget, and use exact scans for small scopes. [Qdrant's write-up](https://qdrant.tech/articles/vector-search-filtering/) explains filtering before versus after the search.
- **Treat the index as something you can rebuild.** The raw text and metadata are the source of truth. This is the fifth time this theme has come up.
- **Refresh database statistics after bulk loads.** Without them, gbrain's searches timed out and fell back to keyword-only.
- **A cheap win:** in gbrain's tests, storing vectors as 16-bit numbers (`halfvec`) kept the same recall with an index about a third smaller.
- **Who owns it:**
  - *Architects* own the index contract (required fields, model version and ACL field) and the runbook for reindexing and rollback.
  - *Product* sets freshness and recall targets per use case, and decides when a reindex is worth a temporary dip in quality.
  - *Devs* own the alias-switch script, one migration per embedding model, and a recall-audit step in CI.

## Sources

- [pgvector](https://github.com/pgvector/pgvector)
- [Qdrant filtering](https://qdrant.tech/articles/vector-search-filtering/)
- [index alias](https://learn.microsoft.com/en-us/azure/search/search-how-to-alias)