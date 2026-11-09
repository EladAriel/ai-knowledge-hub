# PIPE-019: Pipeline: enrichment with three-way entity resolution

## Summary

Extract entities against a schema (GLiNER first, LLM only for what's left), normalize + alias check, vector-search candidates of the same type, score, then merge / send to review / create new; tag against a fixed taxonomy; publish to index and graph.

## Details

parsed chunks -> extract entities against a schema (GLiNER first, LLM only for leftovers) -> normalize names + alias list -> candidate matches of same type by vector search -> score -> merge / review / new -> merge keeping history and sources -> add tags -> publish to index and graph. Rules: settle easy cases with rules first (case, punctuation, 'Inc.'; known alias = certain match; similarity is a hint, not proof). Three outcomes with per-type thresholds: auto-merge >=0.90, 0.85–0.90 to review, below = new; people stricter than product IDs. Give the judge identifying properties, keep history when merging, check new entities against the whole graph. Use the LLM only for the uncertain middle (pairwise comparison grows with the square of entity count; LLM confidence isn't a probability and shifts across versions; sending personal data to an outside model is a privacy issue). Tag against a fixed taxonomy with definitions + synonyms; never overwrite conflicting definitions, keep them side by side with sources. Follow-up to the 10-24 enrichment pipeline.

## Content

## Pipeline pattern of the day: enrichment with three-way entity resolution

parsed chunks -> extract entities against a schema (GLiNER first, an LLM only for what's left) -> normalize names and check the alias list -> find candidate matches of the same type by vector search -> score them -> merge, send to review, or create a new entity -> merge while keeping history and sources -> add tags -> publish to the index and the graph

- **Settle easy cases with rules first.** Normalize case, punctuation and suffixes like "Inc.", and treat a known alias as a certain match. Similarity scores are hints, not proof that two names mean the same thing ([Neo4j resolution docs](https://neo4j.com/labs/agent-memory/explanation/resolution-deduplication/)).
- **Use three outcomes, with thresholds per entity type.** Merge automatically at 0.90 or above, send 0.85–0.90 to review, and create a new entity below that. People need stricter thresholds than product IDs ([Neo4j tuning guide](https://neo4j.com/labs/agent-memory/how-to/tune-entity-resolution/)).
- **Give the judge identifying properties, not metadata, and keep history when merging.** Check new entities against the whole graph, keep the losing values as history, and keep aliases searchable ([FalkorDB](https://www.falkordb.com/blog/knowledge-graph-entity-resolution/)).
- **Use the LLM only for the uncertain middle.** Comparing every pair grows with the square of the entity count. LLM confidence isn't a real probability and can shift between model versions, and sending personal data to an outside model is a privacy issue ([Datasumi](https://www.datasumi.com/blog/knowledge-graphs-ontologies-entity-resolution-enterprise-chatbots)).
- **Tag against a fixed taxonomy, and never overwrite conflicting definitions.** Give the LLM each term's definition and synonyms ([Enterprise Knowledge](https://enterprise-knowledge.com/how-to-leverage-llms-for-auto-tagging-content-enrichment/)). Keep conflicting definitions side b...nce when data comes in, producing structured pieces the agent reads later.
- **Claim–evidence leaf:** one small fact stored with its word-for-word source quote.
- **Sufficiency rate:** the share of questions the stored claims can answer on their own.
- **Review band:** the middle range of match scores, where a possible duplicate goes to a person instead of being merged or created automatically.
- **Alias gazetteer:** a maintained list of known alternate names, like code names, tickers and product codes, that count as a certain match.
- **Identifying property:** a field that tells look-alike entities apart, like birth year, ticker or employee ID.
- **Pending SAME_AS link:** a graph link marking a suggested duplicate nobody has confirmed yet.
- **Semantic model (metric view):** a governed definition of a business metric that already exists in a tool like dbt, LookML or Snowflake.
- **Matryoshka embeddings (MRL):** vectors where a shorter slice from the start is a coarser but still usable embedding.
- **Boundary extraction:** finding an entity by predicting where it starts and ends, so there's no length limit (GLiNER2.5).
- **Jaccard@k:** how much the top-k docs overlap between two rewordings of the same question.
- **Worst-variant accuracy:** a question only passes if every rewording of it is answered correctly.

**Recurring themes:**
- A simple search loop beat fancier structures again, after Memory Tax and the raw-RAG results.
- Rules come first, then the LLM for the uncertain middle, then human review before writing to shared knowledge.
- Conflicting versions are kept with their sources instead of being overwritten.
- More vendors keep launching context layers, including Google's Knowledge Catalog and SAP's Ontology Manager, which I've only seen mentioned in a post on X.

**Rebrand watch:** "knowledge compilation" is enrichment at indexing time, and an LLM judge for merging entities is the classic record-linkage review step.

## Sources

- [Neo4j resolution docs](https://neo4j.com/labs/agent-memory/explanation/resolution-deduplication/)
- [Neo4j tuning guide](https://neo4j.com/labs/agent-memory/how-to/tune-entity-resolution/)
- [FalkorDB](https://www.falkordb.com/blog/knowledge-graph-entity-resolution/)
- [Datasumi](https://www.datasumi.com/blog/knowledge-graphs-ontologies-entity-resolution-enterprise-chatbots)
- [Enterprise Knowledge auto-tagging](https://enterprise-knowledge.com/how-to-leverage-llms-for-auto-tagging-content-enrichment/)