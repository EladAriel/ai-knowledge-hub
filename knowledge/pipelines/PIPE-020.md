# PIPE-020: Pipeline: embedding model upgrade as an index migration

## Summary

Treat an embedding-model change as a schema migration: new versioned index or vector field, dual-write, backfill from source text, shadow-test, gradual traffic shift, keep the old index for rollback.

## Details

Stages: stored source text -> new versioned index or vector field (v2) -> write new docs to both indexes -> backfill v2 from the source text -> test v2 on real queries in the background -> move traffic over gradually -> keep v1 for rollback -> drop v1. Rules: make model version part of the index schema; never mix old and new vectors in one search space (same-size vectors from different models aren't comparable). Re-embed from stored source text and chunking rules, never from old vectors. Two setups: full second index (blue-green; clean, but duplicates data, deletes need care during the switch) or a second vector field on the same records (lighter; Zilliz adds an empty field that fills during backfill; Qdrant named vectors).

## Sources

- [nalar.dev: embedding changes as index migrations](https://nalar.dev/treat-embedding-model-changes-as-index-migrations/)
- [Qdrant embedding model migration guide](https://qdrant.tech/documentation/tutorials-operations/embedding-model-migration/)
- [Zilliz: migrate to a new embedding model](https://docs.zilliz.com/docs/migrate-to-a-new-embedding-model)
