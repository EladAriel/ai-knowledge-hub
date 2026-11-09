# TOOL-034: Repos: Qdrant, Vespa, pgvectorscale

## Summary

Vector DB with named vectors for migrations; one engine for BM25 + vector + multi-stage ranking with a RAG Blueprint; disk-based vector index for Postgres with label-filtered search.

## Details

qdrant/qdrant (~35k stars, v1.20.0 Oct 22, Apache-2.0): borrow named vectors to keep old and new embeddings on the same record during a migration; its migration guide is the best short runbook. Run: docker run -p 6333:6333 qdrant/qdrant. Best for Devs and Architects. vespa-engine/vespa (~7.2k stars, production grade, Apache-2.0, steep learning curve): borrow the RAG Blueprint: index title and chunk embeddings plus text, rank in stages (cheap first pass, costly second pass on a capped set, final merge of result lists). Best for Architects choosing a reference stack. timescale/pgvectorscale (~3.2k stars, v0.9.1, PostgreSQL license): borrow label-filtered search (fits access-control or source labels). Run: CREATE EXTENSION vectorscale CASCADE; Best for Devs who want to stay on Postgres.

## Content

**[qdrant/qdrant](https://github.com/qdrant/qdrant)** is a vector database with rich filtering on stored fields.
- What to borrow: named vectors, which let you keep the old and new embedding on the same record during a migration. Its [migration guide](https://qdrant.tech/documentation/tutorials-operations/embedding-model-migration/) is the best short runbook I found.
- To run it: `docker run -p 6333:6333 qdrant/qdrant`
- Maturity: about 35k stars, v1.20.0 released Oct 22, Apache-2.0.
- Best for: Devs and Architects.

**[vespa-engine/vespa](https://github.com/vespa-engine/vespa)** runs keyword (BM25) search, vector search and multi-stage ranking in one engine.
- What to borrow: the [RAG Blueprint](https://docs.vespa.ai/en/learn/tutorials/rag-blueprint.html). It indexes title and chunk embeddings plus the text, then ranks in stages:
  - a cheap first pass
  - a costly second pass on a capped number of results
  - a final step that merges the result lists
- Maturity: production grade, about 7.2k stars, pushed today, Apache-2.0. It takes real effort to learn.
- Best for: Architects choosing a reference stack.

**[timescale/pgvectorscale](https://github.com/timescale/pgvectorscale)** is a disk-based vector index for Postgres.
- What to borrow: search filtered by labels, which fits access-control or source labels naturally.
- To run it: `CREATE EXTENSION vectorscale CASCADE;`
- Maturity: about 3.2k stars, v0.9.1, PostgreSQL license.
- Best for: Devs who want to stay on Postgres.

## Sources

- [qdrant/qdrant](https://github.com/qdrant/qdrant)
- [vespa-engine/vespa](https://github.com/vespa-engine/vespa)
- [Vespa RAG Blueprint](https://docs.vespa.ai/en/learn/tutorials/rag-blueprint.html)
- [timescale/pgvectorscale](https://github.com/timescale/pgvectorscale)
- [migration guide](https://qdrant.tech/documentation/tutorials-operations/embedding-model-migration/)