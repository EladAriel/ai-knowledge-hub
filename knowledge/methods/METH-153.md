# METH-153: New terms (Nov 14, enterprise knowledge): context reranking, relational flip, agent-sized k, snippet recall, phased ranking, schema briefing

## Summary

One-line terms (Nov 14) on the retrieval and reranking stage.

## Details

Context reranking: the reranker gets the query plus a few sentences on the agent's goal, while filters stay in the engine. Relational flip: the same query and documents with the asked-for direction reversed. Agent-sized k: measuring recall at the number of results the agent actually reads, like 16. Snippet recall: whether the passage that was cited made it into the context. Comparison ranking: how much the top results reorder between two versions of the system. Phased ranking: a cheap wide search first, then a learned ranker, then an expensive reranker on the top few. Source routing F1: a score for how well the agent picks the right sources. Schema briefing: a short description of the tables, keys and links, given to the agent before it plans. Recurring themes: picking the right source (Wayfinder yesterday, RetailBridge today); keeping permissions out of the model and the reranker; for agents, getting the right document into the results matters more than ranking it first.

## Sources

- No single link was recorded for this terms list. Related public sources (see PIPE-031, METH-149 to METH-152):
- [Glean: how to evaluate agent retrieval](https://www.youtube.com/watch?v=hzWv-apa4k4)
- [SwitchIR](https://arxiv.org/abs/2611.15417)
- [RetailBridge](https://arxiv.org/abs/2610.25096)
- [AsteroRank](https://blog.asteromorph.com/asterorank/)
