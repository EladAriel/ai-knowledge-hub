# METH-090: Optimal Re-Ranking Depth: query-specific rerank window, not a fixed top-50

## Summary

Many queries have a best rerank depth; past it, more candidates add nothing or make results worse. An LLM-graded score of first-stage results cut average depth by up to 3x at the same quality; perfect depth choices improved MS MARCO by >7% at 1/5 the depth.

## Details

University of Waterloo paper; code and grades public. Usual query-difficulty predictors failed at picking the depth. Effort: medium. Adopt for: Architects make rerank depth a per-query setting in the retrieval contract; Product tracks cost and latency per answer next to quality; Devs log first-stage scores now to train a depth predictor later.

## Sources

- [Optimal Re-Ranking Depth (arXiv)](https://arxiv.org/abs/2611.05908)
