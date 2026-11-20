# METH-169: MemCredit: pick memory by how much it helps the next decision, not by similarity

## Summary

Measure in counterfactual experiments how much each memory item affects the next action, and train a small model that estimates that utility. At runtime, semantic similarity only finds candidates, and the predicted utility decides what enters the token budget. Promoted from the Nov 14 terms list. arXiv 2611.15600.

## Details

This is close to learned reranking, but the label is utility measured in an experiment, not relevance, and the agent's policy does not change. Evidence: on ALFWorld, with a 500-token budget, 86.57% success versus 65.67% with BM25. The numbers are self-reported, and the source note cuts off after "the test was added only on WebS". The Nov 14 terms line reported 86.6% versus 65.7% of BM25 on ALFWorld.

## Sources

- [MemCredit (arXiv)](https://arxiv.org/abs/2611.15600)
