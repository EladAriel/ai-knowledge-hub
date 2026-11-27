# EVAL-048: Eval: rerank depth sweep

## Summary

An under-a-day eval (Nov 25). Take 50 test questions with known answers. Measure first-stage recall at 20, 50 and 100, then how often the right passage is in the top 5 after reranking each pool, plus the latency of each. Pick the smallest pool where that top-5 score stops rising. That gives you quality per millisecond, not a guess.

## Details

What it catches: a rerank window that is larger than it needs to be, or a first-stage pool that is too small for the reranker to recover the right passage.

Related: METH-090 studies a query-specific rerank window, not this fixed sweep on your own questions. Complements the retrieval practice in PIPE-040 and METH-213.

Effort: under a day.

## Sources

- [Rerank once per search step (METH-213)](https://arxiv.org/abs/2611.32917)
- [PIPE-040: wide hybrid pool, rerank against the original question](../pipelines/PIPE-040.md)
