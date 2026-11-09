# TOOL-034: Repos: Qdrant, Vespa, pgvectorscale

## Summary

Vector DB with named vectors for migrations; one engine for BM25 + vector + multi-stage ranking with a RAG Blueprint; disk-based vector index for Postgres with label-filtered search.

## Details

qdrant/qdrant (~35k stars, v1.20.0 Oct 22, Apache-2.0): borrow named vectors to keep old and new embeddings on the same record during a migration; its migration guide is the best short runbook. Run: docker run -p 6333:6333 qdrant/qdrant. Best for Devs and Architects. vespa-engine/vespa (~7.2k stars, production grade, Apache-2.0, steep learning curve): borrow the RAG Blueprint: index title and chunk embeddings plus text, rank in stages (cheap first pass, costly second pass on a capped set, final merge of result lists). Best for Architects choosing a reference stack. timescale/pgvectorscale (~3.2k stars, v0.9.1, PostgreSQL license): borrow label-filtered search (fits access-control or source labels).

## Sources

- [qdrant/qdrant](https://github.com/qdrant/qdrant)
- [vespa-engine/vespa](https://github.com/vespa-engine/vespa)
- [Vespa RAG Blueprint](https://docs.vespa.ai/en/learn/tutorials/rag-blueprint.html)
- [timescale/pgvectorscale](https://github.com/timescale/pgvectorscale)
