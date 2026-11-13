# METH-133: New terms (Nov 11): Claude Data / certified queries, ShadowBench-MCP, PAF, Synapse-Control, CAMP-II / CAMG-II, trace-based evaluation

## Summary

One-line mentions from the Nov 11 AI methods digest (no full evaluations). Muse Ember is repeated from Nov 10 and is not listed again. ENGRAM (already METH-112) is only a same-day pointer.

## Details

Claude Data / certified queries (claude.com/resources/articles/sheets-whiteboards-data): metrics a data team approves and marks as certified, with live sharing that does not expose the connectors—in practice a managed semantic layer inside the chat. Gemini 4 Carbon and the /swarm command in Antigravity: open to everyone; the price doubles on 1.12. ShadowBench-MCP (arXiv 2611.11720): checks whether a tool router picks a path that skips controls; this happened in 29.2% of cases when the policy favoured efficiency, and 4.2% when it took the rules into account; tested on a single router. PAF, Portable Agent Format (2611.13055): a work product packed with its context, evidence and access rules; 96% vs 86% for RAG on the raw files. Synapse-Control (2611.13615): a 1.7B classifier that picks advice from a list instead of generating a diagnosis, and a prompt-value table that prevents repetition. ENGRAM (2611.09472): already METH-112; mentioned again as folding experience into model weights, with a verification step before deleting external memory. CAMP-II / CAMG-II (2611.14009): file-based memory training for coding agents via on-policy distillation. Comparison of evaluation methods (2611.14493, KDD): evaluation that reads the run trace reached F1 of 0.90, and evaluation of the text alone produced 5 times as many false alerts.

## Sources

- [Claude Data / certified queries](https://claude.com/resources/articles/sheets-whiteboards-data)
- [ShadowBench-MCP](https://arxiv.org/abs/2611.11720)
- [PAF](https://arxiv.org/abs/2611.13055)
- [Synapse-Control](https://arxiv.org/abs/2611.13615)
- [CAMP-II / CAMG-II](https://arxiv.org/abs/2611.14009)
- [trace vs text evaluation (KDD)](https://arxiv.org/abs/2611.14493)
