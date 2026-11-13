# PIPE-028: Pipeline: enrichment and entity resolution

## Summary

pull out names using a fixed ontology -> clean up names and match aliases -> shortlist about 10 likely matches per record with vector search -> score each pair -> merge automatically, send to a person, or create a new entity -> one writer saves to the graph, keeping each fact's source.

## Details

Cheap rules first, the LLM only for unclear cases. Exact and alias matching handles most records. In Actian's write-up (a vendor post): shortlisting cut candidate pairs from 1.18M to 10.8k while keeping 99% of true matches; the LLM reviewed only the unclear 13.2%; quality (F1) rose from 0.813 to 0.915, at about $0.76 per 1,000 records. Extract in parallel, but have only one writer—if two writers handle the same name at once, you get duplicate entities (Dynamiq docs). Match on the whole entity, not just the name; compare type and attributes too, so you merge by identity, not spelling (Decoding AI). Give each match a status (proposed, ready, committed), so human review can happen in the background (BoundaryML, from 2025 but still holds). Save category links during enrichment; per CLADE, they let you answer from vague evidence later. Owners: Architects own the master list of entities and the rules for merging or splitting them; Product decides who staffs the review queue and how fast it must clear, for example within 48 hours for customers and people; Devs build one resolve() function with fixed inputs and outputs, swappable matchers, and a labeled test set in CI. New in the pipeline rotation on Nov 11 (enrichment stage).

## Sources

- [Actian write-up](https://www.actian.com/blog/developer/how-we-did-entity-resolution-with-a-vector-db-and-argon/)
- [Dynamiq docs](https://docs.getdynamiq.ai/docs/sdk/rag/knowledge-graphs)
- [Decoding AI](https://www.decodingai.com/p/keep-knowledge-graph-clean)
- [BoundaryML (2025)](https://boundaryml.com/podcast/2025-06-17-entity-extraction)
