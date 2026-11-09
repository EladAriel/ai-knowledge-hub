# METH-019: Always rerank; agentic search only once tuned (Kapa Company Knowledge Bench)

## Summary

7 retrievers on 1,000 production queries: hybrid 0.41, top-100 reranked to 15 = 0.50 for ~0.3 s and no extra tokens.

## Details

Sub-query split 0.56 (1.8 s). Frontier model with grep only 0.61 but 13-17 s, ~$0.17/query, ~40k tokens (1 in 25 chunks needed); Kapa agentic retriever 0.65 in ~5 s, ~5k tokens. ….

## Sources

- [Kapa Company Knowledge Bench](https://www.kapa.ai/blog/company-knowledge-bench)
