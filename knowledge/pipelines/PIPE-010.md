# PIPE-010: Pipeline: enrichment (extraction + entity resolution)

## Summary

chunk -> extract against typed schema -> link each value to source position -> drop out-of-schema items -> resolve ….

## Details

Typed schema with a named owner, checked against the ontology (cognee, FalkorDB prune step). Every entity/relation keeps source chunk ID and position (citations, cascading deletes, re-extraction). ….

## Sources

- [cognee ontology retrieval](https://www.cognee.ai/custom-ontology-rag-retrieval)
- [FalkorDB GraphRAG](https://docs.falkordb.com/graphrag/architecture)
- [Deg-RAG](https://arxiv.org/abs/2510.14271)
