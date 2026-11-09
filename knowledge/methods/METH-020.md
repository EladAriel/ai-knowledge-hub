# METH-020: GraphRAG indexing cost reality check

## Summary

GraphRAG on one 41-page paper with a local 27B model: ~281 calls, ~2 h; another 26-page paper +73 min; the graph is an ongoing cost.

## Details

6 in 10 entities were people (bibliography chunks); the target relation was extracted once. HippoRAG failure analysis: 48% of errors from entity spotting, 28% from relation extraction. Caveat: 8-question comparison judged by same model. Before approving a graph layer require indexing cost per doc and freshness plan; filter bibliography/boilerplate before extraction; fund graphs only for relationship/whole-collection questions.

## Content

**4. [Should we put a knowledge graph under our RAG?](https://x.com/sermakarevich/status/2111515269638074660)** (Sergii Makarevych on X, Oct 17, with a [runnable Neo4j tutorial](https://github.com/sermakarevich/tutorials/tree/main/graph_rag))
- He built GraphRAG from one 41-page paper with a local 27B model. It took about 281 chat calls and about 2 hours, 70 minutes of which went to entity extraction. Adding one more 26-page paper cost another 73 minutes, so the graph is an ongoing cost, not a one-time build.
- Six in ten entities ended up being people, because about 50 of the 146 chunks were the bibliography. The relationship the graph was built for ("method tested on dataset") was extracted exactly once.
- He cites HippoRAG's failure analysis: 48% of errors came from spotting entities and 28% from extracting relationships. So most graph failures happen before any graph algorithm runs.
- Caveat: his own head-to-head used only 8 questions, judged by the same model, so read it as a careful field report, not a benchmark. His warning that GraphRAG proposals usually skip the indexing cost is fair.
- Adopt for:
  - *Architects:* before approving a graph layer, require an estimate of indexing cost per document and a plan for keeping the graph fresh.
  - *Product:* fund a graph only for questions about relationships or the whole collection, like "which X relate to Y" or "what are the main themes."
  - *Devs:* before building on the graph, check how often each relationship type appears, and filter out bibliography and boilerplate chunks before extraction.

## Sources

- [Sergii Makarevych on X](https://x.com/sermakarevich/status/2111515269638074660)
- [Neo4j tutorial](https://github.com/sermakarevich/tutorials/tree/main/graph_rag)