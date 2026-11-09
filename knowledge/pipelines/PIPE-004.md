# PIPE-004: Pipeline: retrieval and reranking

## Summary

query -> optional rewrite/split -> ACL pre-filter -> BM25 + vector (top 100-200) -> RRF (k=60) -> rerank to ~15 -> expand to parent section -> compress/token budget -> agent.

## Details

Always rerank (retrieve ~100, cut ~15). RRF merges keyword and vector without score normalization (k=60, as in RIT-RAG). Split chunks at section boundaries and store the section path to expand to the full section. Route by difficulty: fixed pipeline by default, query split/agentic loops for hard questions. Measure tokens returned per query next to accuracy. Devs own a version-controlled retrieval config plus recall@k and tokens-returned check in CI.

## Content

## Pipeline pattern of the day: retrieval and reranking

query -> optional query rewrite or split -> ACL pre-filter -> BM25 + vector search (top 100 to 200 each) -> RRF merge (k=60) -> reranker (down to about 15) -> expand to the parent section or doc tree -> compress or apply a token budget -> agent

- **Always rerank.** Retrieve wide (around 100) and cut narrow (around 15). In Kapa's test this took the score from 0.41 to 0.50 for about 0.3 s ([Kapa](https://www.kapa.ai/blog/company-knowledge-bench)).
- **Use RRF to merge keyword and vector results.** It needs no score normalization, and k=60 is the standard setting, the same one RIT-RAG used ([RIT-RAG](https://arxiv.org/abs/2610.11370)).
- **Split chunks at section boundaries and store the section path on each chunk,** so you can expand to the full section. This fixes chunks that cut a table in half, and the RIT-RAG paper shows a balance sheet split exactly that way.
- **Route queries by difficulty.** Use the fixed pipeline by default, and save query splitting or agentic loops for hard or high-value questions. Agentic grep took 13 to 17 s and returned about 40k tokens per query.
- **Measure tokens returned per query next to accuracy.** Every extra chunk costs money and makes reasoning harder.
- **Who owns what:**
  - *Architects* own the retrieval API contract (filters go in, ranked chunks with authority, freshness and section path come out), the policy for swapping rerankers, and the rule that the ACL filter runs before ranking.
  - *Product* owns routing: which use cases get the fast path and which get the deep path, plus a latency and cost budget for each.
  - *Devs* own the code: a version-controlled retrieval config with top-k, merge settings and reranker model, plus a recall@k and tokens-returned check in CI on every config change.

## Sources

- [RIT-RAG](https://arxiv.org/abs/2610.11370)
- [Kapa](https://www.kapa.ai/blog/company-knowledge-bench)