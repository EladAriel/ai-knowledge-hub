# METH-119: Decision Context (forge_dc): behavioral memory injected at decision points

## Summary

The system captures user corrections and tool-call failures and turns them into written rules. It injects each rule only at the decision point where it is relevant. Accepted to the PALM workshop at NeurIPS 2026.

## Details

What's new: most memory systems store facts; this stores ways of acting. Close to WASP-Mem (Nov 4), but the emphasis is on injection placement. Author-reported: 95% rule adherence vs 55% with plain retrieval, at 10x fewer tokens. The benchmark (DC-Bench, 71 scenarios) was built by the authors. Recommendation: Pilot. The memory theme has recurred almost daily (Nov 4, 6 and 8). arXiv 2611.08644.

## Sources

- [Decision Context / forge_dc (arXiv)](https://arxiv.org/abs/2611.08644)
