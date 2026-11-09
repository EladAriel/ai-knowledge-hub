# PIPE-010: Pipeline: enrichment (extraction + entity resolution)

## Summary

chunk -> extract against typed schema -> link each value to source position -> drop out-of-schema items -> resolve duplicates -> human review for low confidence -> write with entity->chunk link -> index.

## Details

Typed schema with a named owner, checked against the ontology (cognee, FalkorDB prune step). Every entity/relation keeps source chunk ID and position (citations, cascading deletes, re-extraction). Entity resolution shrinks the graph and improves QA (Deg-RAG). Re-extract only docs whose content hash changed. Separate read and write paths with tighter write permissions. Product picks 5-10 entity types first.

## Content

## Pipeline pattern of the day: enrichment

chunk -> extract against a typed schema -> link each value to its source position -> drop items outside the schema -> resolve duplicate entities (group candidates, match, merge) -> human review for low-confidence items -> write, with a link from each entity to the chunk it came from -> index

- **Extract against a typed schema with a named owner, and check results against the ontology.** See [cognee's ontology retrieval](https://www.cognee.ai/custom-ontology-rag-retrieval) and the [FalkorDB GraphRAG pipeline](https://docs.falkordb.com/graphrag/architecture), which has a built-in step that removes items outside the schema.
- **Give every entity and relationship its source chunk ID and position.** That link is what makes citations, cascading deletes and re-extraction possible.
- **Don't underestimate entity resolution.** Merging duplicate entities shrinks the graph and improves question answering across GraphRAG variants ([Deg-RAG](https://arxiv.org/abs/2510.14271)).
- **Only re-extract docs whose content hash changed,** so you pay only for what changed. This ties back to yesterday's chunk-update-cost paper.
- **Keep reading the graph and writing to it as separate paths,** with tighter permissions on writes.
- **Who owns it:**
  - *Architects* own the ontology, the schema contract, the source-link fields and the delete cascade.
  - *Product* picks the 5–10 entity types that drive real use cases (such as customer, contract, product and owner) before anyone models everything.
  - *Devs* build one tested extraction module per entity type, a source-position check like LangExtract's, and Splink or alias matching that runs before an LLM decides.

## Sources

- [cognee ontology retrieval](https://www.cognee.ai/custom-ontology-rag-retrieval)
- [FalkorDB GraphRAG](https://docs.falkordb.com/graphrag/architecture)
- [Deg-RAG](https://arxiv.org/abs/2510.14271)