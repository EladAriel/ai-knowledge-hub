# PIPE-019: Pipeline: enrichment with three-way entity resolution

## Summary

Extract entities against a schema (GLiNER first, LLM only for what's left), normalize + alias check, vector-search candidates of the same type, score, then merge / send to review / create new; tag against a fixed taxonomy; publish to index and graph.

## Details

parsed chunks -> extract entities against a schema (GLiNER first, LLM only for leftovers) -> normalize names + alias list -> candidate matches of same type by vector search -> score -> merge / review / new -> merge keeping history and sources -> add tags -> publish to index and graph. Rules: settle easy cases with rules first (case, punctuation, 'Inc.'; known alias = certain match; similarity is a hint, not proof). Three outcomes with per-type thresholds: auto-merge >=0.90, 0.85–0.90 to review, below = new; people stricter than product IDs. Give the judge identifying properties, keep history when merging, check new entities against the whole graph. Use the LLM only for the uncertain middle (pairwise comparison grows with the square of entity count; LLM confidence isn't a probability and shifts across versions; sending personal data to an outside model is a privacy issue).

## Sources

- [Neo4j resolution docs](https://neo4j.com/labs/agent-memory/explanation/resolution-deduplication/)
- [Neo4j tuning guide](https://neo4j.com/labs/agent-memory/how-to/tune-entity-resolution/)
- [FalkorDB](https://www.falkordb.com/blog/knowledge-graph-entity-resolution/)
- [Datasumi](https://www.datasumi.com/blog/knowledge-graphs-ontologies-entity-resolution-enterprise-chatbots)
- [Enterprise Knowledge auto-tagging](https://enterprise-knowledge.com/how-to-leverage-llms-for-auto-tagging-content-enrichment/)
