# METH-049: Scoped vector search collapses recall under ACL filters (gbrain)

## Summary

At a 10% scope, Postgres HNSW recall@50 fell to 0.52-0.77; raising scan budget 2,000 -> 20,000 rows restored 0.96-0.99 for +16-36 ms.

## Details

Hardest case (10% scope, shared topics) still 0.78: exact search first or a separate index per source. Skipping DB statistics after bulk import pushed 44-100% of scoped searches past the 8 s budget (keyword fallback). Keep ef_search/scan budget in versioned config; run ANALYZE after every bulk load; decide partition/exact scan/shared index per tenant.

## Content

**1. [gbrain: scoped vector search at 1–2M chunks](https://github.com/garrytan/gbrain-evals/blob/main/docs/benchmarks/2026-10-09-hnsw-scale.md)**
- **What happened:** with results limited to a 10% scope (basically an ACL filter), Postgres HNSW recall@50 fell to 0.52–0.77. HNSW is the common graph-based vector index, and recall@50 is the share of the true top 50 it returns. Raising the per-search scan budget from 2,000 to 20,000 rows brought recall back to 0.96–0.99, at a cost of 16–36 ms more per search.
- **Hardest case:** a 10% scope where every doc shares topics, like one department's docs, still only reached 0.78. The fix there is an exact search first, or a separate index per source.
- **Another catch:** skipping database statistics after a bulk import pushed 44–100% of scoped searches past the 8-second budget, so they fell back to keyword-only.
- Adopt for:
  - *Architects:* decide per tenant or source whether it gets its own partition, an exact scan, or the shared index, based on its size and how clustered its topics are.
  - *Product:* "users get fewer or worse answers in their own space" is a real failure. Track it per team, not just overall.
  - *Devs:* keep the `ef_search` and scan-budget settings in versioned config, and run `ANALYZE` after every bulk load.

## Sources

- [gbrain HNSW scale benchmark](https://github.com/garrytan/gbrain-evals/blob/main/docs/benchmarks/2026-10-09-hnsw-scale.md)