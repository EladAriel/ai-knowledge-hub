# METH-071: Routed Continual Learning (FAIR, Meta)

## Summary

Before each run an LLM router picks the memory 'cluster' and memory type (full-history ICL, ReasoningBank or a statistical model); memory is injected into context without changing the agent.

## Details

Treats continual learning as a routing problem instead of one global memory: what to keep and whom to share with is decided per task. Tested on 398 mixed tasks from CL-Bench and τ³-Bench, 4 models, 5 runs: beats Global ICL by 15-30% of max reward at 65-72% lower API cost; Global ICL barely helps when tasks are mixed. Limits: no parallel updates or cross-model memory tested; router sometimes over-splits (23-86 clusters). Fit: high for enterprise assistants serving many task types.

## Sources

- [Routed Continual Learning](https://arxiv.org/abs/2610.38796)
