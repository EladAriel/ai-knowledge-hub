# METH-092: RAGCompass: choose a retriever by reading the passages it returned

## Summary

Picks which retriever to trust by reading the passages each one returned, not just the question. A reranker is trained on which set of passages led to the right answer. Answer F1 rose 28% over the best single retriever; beat merging all results and choosing from the question alone; kept most of the gain on unseen docs and retrievers.

## Content

## Pipeline pattern of the day: retrieval and reranking with a flexible budget
- **Route by source.** Compare the results different retrievers return, not just the question ([RAGCompass](https://arxiv.org/abs/2611.05596)).

## Sources

- [RAGCompass (arXiv)](https://arxiv.org/abs/2611.05596)