# PIPE-011: Pipeline: indexing with alias switch and rollback

## Summary

chunks + metadata (doc_id, version, acl, embed_model) -> versioned store -> build vector/BM25/graph into a NEW index -> ….

## Details

Never mix embedding models in one index; store model+version per row; rebuild and switch an index alias. Filtered search trap: pgvector filters after the scan (10% filter with ef_search 40 returns ~4 rows) -> iterative index ….

## Sources

- [pgvector](https://github.com/pgvector/pgvector)
- [Qdrant filtering](https://qdrant.tech/articles/vector-search-filtering/)
- [index alias](https://learn.microsoft.com/en-us/azure/search/search-how-to-alias)
