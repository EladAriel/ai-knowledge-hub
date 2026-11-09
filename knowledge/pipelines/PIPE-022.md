# PIPE-022: Pipeline: retrieval and reranking with a flexible budget

## Summary

question -> hybrid keyword+vector search -> top N candidates -> cross-encoder rerank -> drop under a minimum score -> pass top k in order to the LLM. Make rerank depth an explicit setting; use a calibrated minimum score, not just fixed k; adjust depth per query; route by source (RAGCompass); swap rerankers only after the golden set passes.

## Details

Azure AI Search reranks only top 50; Elastic has rank_window_size. Cohere recipe: rerank 20, keep top 5, drop under a min score (needs calibrated scores). Who owns it: Architects own the retrieval contract (candidates, min score, k, which retrievers); Product owns quality/speed/cost targets per use case; Devs ship one config file per use case, a local reranker for CI, and scores logged at every stage.

## Sources

- (no public source link recorded)
