# PIPE-020: Pipeline: embedding model upgrade as an index migration

## Summary

Treat an embedding-model change as a schema migration: new versioned index or vector field, dual-write, backfill from source text, shadow-test, gradual traffic shift, keep the old index for rollback.

## Details

Stages: stored source text -> new versioned index or vector field (v2) -> write new docs to both indexes -> backfill v2 from the source text -> test v2 on real queries in the background -> move traffic over gradually -> keep v1 for rollback -> drop v1. Rules: make model version part of the index schema; never mix old and new vectors in one search space (same-size vectors from different models aren't comparable). Re-embed from stored source text and chunking rules, never from old vectors. Two setups: full second index (blue-green; clean, but duplicates data, deletes need care during the switch) or a second vector field on the same records (lighter; Zilliz adds an empty field that fills during backfill; Qdrant named vectors). Switch the query embedder and the vector field together; move traffic in steps watching quality, latency and errors. Re-tune score thresholds and hybrid weights after any model change; keep keyword search for IDs, error codes, product codes. Owners: Architects own a registry of index versions (model, vector size, similarity, chunker version) and the rollback policy; Product sets the switch bar (e.g. 'no worse on our top 50 real questions'); Devs own scripted migration jobs, a dual-write flag and one config switch for the serving index. Terms: alias flip, dual-write, blue-green, named vectors, embedding-space mapping (learned translator between two models' vectors).

## Content

## Pipeline pattern of the day: an embedding model upgrade as an index migration

stored source text -> new versioned index or vector field (v2) -> write new docs to both indexes -> backfill v2 from the source text -> test v2 on real queries in the background -> move traffic over gradually -> keep v1 for rollback -> drop v1

- **Make the model version part of the index schema.** Never mix old and new vectors in one search space, because vectors of the same size from different models still can't be compared ([nalar.dev](https://nalar.dev/treat-embedding-model-changes-as-index-migrations/)).
- **Re-embed from the stored source text and chunking rules, never from old vectors.** This is another reason to keep raw text and make chunking reproducible.
- **Pick one of two setups** ([Qdrant](https://qdrant.tech/documentation/tutorials-operations/embedding-model-migration/)):
  - A full second index (blue-green) is clean, but it duplicates the stored data, and deletes need care during the switch.
  - A second vector field on the same records is lighter. [Zilliz](https://docs.zilliz.com/docs/migrate-to-a-new-embedding-model) adds an empty field that fills in as you backfill.
- **Switch the query embedder and the vector field together,** and move traffic in steps while watching quality, latency and errors.
- **Re-tune score thresholds and hybrid weights after any model change,** because the scores shift. Keep keyword search for IDs, error codes and product codes.
- **Who owns it:**
  - *Architects* own a registry of index versions (model, vector size, similarity measure, chunker version) and the rollback policy.
  - *Product* sets the bar for switching, such as "no worse on our top 50 real questions," and schedules the switch away from busy periods.
  - *Devs* own scripted migration jobs, a flag for writing to both indexes, and one config switch for which index serves queries.

## Sources

- [nalar.dev: embedding changes as index migrations](https://nalar.dev/treat-embedding-model-changes-as-index-migrations/)
- [Qdrant embedding model migration guide](https://qdrant.tech/documentation/tutorials-operations/embedding-model-migration/)
- [Zilliz: migrate to a new embedding model](https://docs.zilliz.com/docs/migrate-to-a-new-embedding-model)