# TOOL-038: Repos: qdrant/fastembed, FlagOpen/FlagEmbedding, castorini/pyserini

## Summary

Three local/reproducible retrieval tools for rerank and baselines. fastembed (~3.3k★, Apache-2.0, pushed Nov 4): runs embedding and cross-encoder rerankers on CPU; borrow TextCrossEncoder for cheap local CI reranks (`pip install fastembed`). FlagEmbedding (~12.3k★, MIT, pushed Oct 27): BGE embedding/rerank models including bge-reranker-v2 and a small Gemma reranker plus training scripts; borrow a self-hosted reranker fine-tuned on your golden pairs.

## Details

fastembed (~3.3k★, Apache-2.0, pushed Nov 4): runs embedding and cross-encoder rerankers on CPU; borrow TextCrossEncoder for cheap local CI reranks (`pip install fastembed`). FlagEmbedding (~12.3k★, MIT, pushed Oct 27): BGE embedding/rerank models including bge-reranker-v2 and a small Gemma reranker plus training scripts; borrow a self-hosted reranker fine-tuned on your golden pairs. pyserini (~2.2k★, Apache-2.0, pushed Nov 4): reproducible BM25 and vector baselines with built-in eval scripts (`pip install pyserini`); borrow BM25 baseline and standard scoring for the golden set.

## Sources

- [fastembed](https://github.com/qdrant/fastembed)
- [FlagEmbedding](https://github.com/FlagOpen/FlagEmbedding)
- [pyserini](https://github.com/castorini/pyserini)
