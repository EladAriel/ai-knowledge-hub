# PIPE-031: Pipeline: retrieval and reranking (agent-sized k, phased ranking, goal to the reranker, route directional questions)

## Summary

question -> agent writes a keyword query plus a short note on its goal -> router picks the store (vector, keyword, SQL or graph) -> wide first search for 100–1,000 candidates, with permission filters inside the engine -> combine the keyword and vector rankings -> cheap learned ranker using signals like keyword score, freshness and source authority -> expensive reranker on the top 50 or so, given the agent's goal -> keep the 8–16 results the agent reads -> pick snippets -> answer with citations

## Details

Choose k for the agent, then tune for recall. The LLM reads every result, so recall in those results matters most, and precision is for later steps (Glean talk). Rank in phases rather than with one big model. Start cheap and wide, add a learned ranker trained on logged signals, and save the expensive reranker for the top results. Vespa says the expensive step matters less for RAG than for classic search. Rerankers judge relevance, not permissions. Keep filters in the engine, and give the reranker the agent's goal (AsteroRank). Send directional and relationship questions to a graph or SQL instead of embeddings (SwitchIR, RetailBridge). Break every metric down by data source. A drop for one source is often a connector or logging bug, not a ranking bug (Glean's Slack story). Owners: Architects own the router rules for which question types go to which store, plus the time and candidate budget for each step; Product owns k, the latency target and the per-source dashboard, and decides which questions get the expensive deep-research profile; Devs keep the ranking profiles in code, log the signals the second ranker uses, and run the golden questions through every profile in CI. Added on Nov 14 (retrieval and reranking stage, fourth time on it).

## Sources

- [Glean: how to evaluate agent retrieval](https://www.youtube.com/watch?v=hzWv-apa4k4)
- [SwitchIR](https://arxiv.org/abs/2611.15417)
- [RetailBridge](https://arxiv.org/abs/2610.25096)
- [AsteroRank](https://blog.asteromorph.com/asterorank/)
