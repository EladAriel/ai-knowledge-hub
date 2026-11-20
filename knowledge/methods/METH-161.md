# METH-161: MAPE: discover agent memory designs by evolving code

## Summary

A loop that diagnoses, proposes changes, and evolves a complete memory program from a minimal starting point. Every memory system is a Python class with build, retrieve and compose stages. The value is not the framework itself, but two patterns the authors verified. Also listed as a repo on Nov 13. Code: ash-ding/MAPE (arXiv 2611.17068).

## Details

The two verified patterns: keep raw conversations as evidence you can retrieve, not only memories extracted from them; and compose the evidence according to what the question asks for. When the authors transplanted the compose component into five existing memory systems (Mem0, A-Mem, LightMem, SimpleMem and Zep share the same interface), all of them improved. Finding: up to 12% more accuracy at 35% of the serving cost, scored on LoCoMo and LongMemEval with the cost of each step. What to borrow: the build, retrieve and compose split as your memory interface, plus the setup for comparing memory systems side by side. Maturity: research code with 2 stars, Apache-2.0, last pushed Nov 9, and the paper is still under review. Best for Devs. A Nov 13 methods review ties this to WikiTrace (Nov 11) and Raw-RAG (Oct 23), which also showed that raw evidence wins.

## Sources

- [MAPE (arXiv)](https://arxiv.org/abs/2611.17068)
- [ash-ding/MAPE](https://github.com/ash-ding/MAPE)
