# PIPE-022: Pipeline: retrieval and reranking with a flexible budget

## Summary

question -> hybrid keyword+vector search -> top N candidates -> cross-encoder rerank -> drop under a minimum score -> pass top k in order to the LLM. Make rerank depth an explicit setting; use a calibrated minimum score, not just fixed k; adjust depth per query; route by source (RAGCompass); swap rerankers only after the golden set passes.

## Details

Azure AI Search reranks only top 50; Elastic has rank_window_size. Cohere recipe: rerank 20, keep top 5, drop under a min score (needs calibrated scores). Who owns it: Architects own the retrieval contract (candidates, min score, k, which retrievers); Product owns quality/speed/cost targets per use case; Devs ship one config file per use case, a local reranker for CI, and scores logged at every stage.

## Content

## Pipeline pattern of the day: retrieval and reranking with a flexible budget

question -> keyword and vector search together -> keep the top N candidates -> rerank them with a cross-encoder -> drop anything under a minimum score -> pass the top k, in order, to the LLM

- **Make rerank depth an explicit setting.** Azure AI Search reranks only the top 50 ([docs](https://learn.microsoft.com/en-us/azure/search/semantic-search-overview)), and Elastic lets you set it with `rank_window_size` ([docs](https://www.elastic.co/docs/reference/elasticsearch/rest-apis/retrievers/text-similarity-reranker-retriever)). Measure on your own data where more depth stops helping.
- **Use a minimum score, not just a fixed k.** Cohere's recipe reranks 20 candidates, keeps the top 5, and drops anything under a minimum score ([post](https://cohere.com/blog/embed-rerank-5-openrouter)). That only works if your reranker's scores are calibrated, meaning they mean the same thing across queries, so check yours.
- **Adjust depth per query.** Easy queries get a short list, and hard ones a long list ([depth paper](https://arxiv.org/abs/2611.05908)). Log first-stage scores so you can learn when to go deeper.
- **Route by source.** Compare the results different retrievers return, not just the question ([RAGCompass](https://arxiv.org/abs/2611.05596)).
- **Swap rerankers safely.** A reranker reads raw text, so swapping one doesn't require rebuilding the index. Still require the golden set to pass first.
- **Who owns it:**
  - *Architects* own the retrieval contract: how many candidates, the minimum score, k, and which retrievers can be routed. Any change needs an eval sign-off.
  - *Product* owns targets for quality, speed and cost per use case. Support search can be shallow and fast, while legal or finance search goes deep.
  - *Devs* ship one config file per use case, a local reranker for CI, and scores logged at every stage.

## Sources

- [docs](https://learn.microsoft.com/en-us/azure/search/semantic-search-overview)
- [docs](https://www.elastic.co/docs/reference/elasticsearch/rest-apis/retrievers/text-similarity-reranker-retriever)
- [post](https://cohere.com/blog/embed-rerank-5-openrouter)
- [depth paper](https://arxiv.org/abs/2611.05908)
- [RAGCompass](https://arxiv.org/abs/2611.05596)