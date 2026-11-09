# PIPE-004: Pipeline: retrieval and reranking

## Summary

query -> optional rewrite/split -> ACL pre-filter -> BM25 + vector (top 100-200) -> RRF (k=60) -> rerank to ~15 -> ….

## Details

Always rerank (retrieve ~100, cut ~15). RRF merges keyword and vector without score normalization (k=60, as in RIT-RAG). Split chunks at section boundaries and store the section path to expand to the full section. ….

## Sources

- [RIT-RAG](https://arxiv.org/abs/2610.11370)
- [Kapa](https://www.kapa.ai/blog/company-knowledge-bench)
