# METH-090: Optimal Re-Ranking Depth: query-specific rerank window, not a fixed top-50

## Summary

Many queries have a best rerank depth; past it, more candidates add nothing or make results worse. An LLM-graded score of first-stage results cut average depth by up to 3x at the same quality; perfect depth choices improved MS MARCO by >7% at 1/5 the depth.

## Content

**1. [Optimal Re-Ranking Depth](https://arxiv.org/abs/2611.05908)** (University of Waterloo)
- **The finding:** many queries have a best rerank depth. Reranking past it adds nothing or makes results worse.
- **What works:** the usual ways of predicting query difficulty failed at picking the depth. An LLM-graded score of the first-stage results did better, cutting average depth by up to 3 times with the same quality.
- **The ceiling:** with perfect depth choices, results improved by more than 7% at one fifth the depth on the MS MARCO benchmark. Code and grades are public.
- Adopt for:
  - *Architects:* make rerank depth a setting per query in the retrieval contract, not a fixed number.
  - *Product:* track cost and latency per answer next to quality.
  - *Devs:* log first-stage scores now, so you can train a depth predictor later.

## Sources

- [Optimal Re-Ranking Depth (arXiv)](https://arxiv.org/abs/2611.05908)
