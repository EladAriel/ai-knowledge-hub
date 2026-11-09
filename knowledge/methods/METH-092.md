# METH-092: RAGCompass: choose a retriever by reading the passages it returned

## Summary

Picks which retriever to trust by reading the passages each one returned, not just the question. A reranker is trained on which set of passages led to the right answer. Answer F1 rose 28% over the best single retriever; beat merging all results and choosing from the question alone; kept most of the gain on unseen docs and retrievers.

## Details

Effort: medium to high. Adopt for: Architects give every retriever (wiki, tickets, code, CRM) the same interface so results can be compared; Product tags golden questions by source type; Devs start simple — run all retrievers, rerank the combined results, and log which source wins.

## Sources

- [RAGCompass (arXiv)](https://arxiv.org/abs/2611.05596)
