# METH-057: Calibrated reranker thresholds (Cohere Rerank 5) and their scale problem

## Summary

Calibrated scores let you keep docs above a threshold (or say 'no evidence'); … Cohere Rerank 5: score ~ probability a doc is useful; Context Focus returns best passages (half the context -2 pts, three-quarters -7 pts; Cohere's numbers, own RCP-nDCG metric).

## Details

Cohere Rerank 5: score ~ probability a doc is useful; Context Focus returns best passages (half the context -2 pts, three-quarters -7 pts; Cohere's numbers, own RCP-nDCG metric). ….

## Sources

- [Cohere Rerank 5](https://cohere.com/blog/rerank-5)
- [The Price of Scale in …](https://arxiv.org/abs/2610.34507)
