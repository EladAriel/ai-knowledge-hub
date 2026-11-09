# METH-049: Scoped vector search collapses recall under ACL filters (gbrain)

## Summary

At a 10% scope, Postgres HNSW recall@50 fell to 0.52-0.77; raising scan budget 2,000 -> 20,000 rows restored 0.96-0.99 ….

## Details

Hardest case (10% scope, shared topics) still 0.78: exact search first or a separate index per source. Skipping DB statistics after bulk import pushed 44-100% of scoped searches past the 8 s budget (keyword fallback). ….

## Sources

- [gbrain HNSW scale benchmark](https://github.com/garrytan/gbrain-evals/blob/main/docs/benchmarks/2026-10-09-hnsw-scale.md)
