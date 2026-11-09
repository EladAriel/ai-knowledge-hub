# TOOL-038: Repos: qdrant/fastembed, FlagOpen/FlagEmbedding, castorini/pyserini

## Summary

Three local/reproducible retrieval tools for rerank and baselines.

## Details

fastembed (~3.3k★, Apache-2.0, pushed Nov 4): runs embedding and cross-encoder rerankers on CPU; borrow TextCrossEncoder for cheap local CI reranks (`pip install fastembed`). FlagEmbedding (~12.3k★, MIT, pushed Oct 27): BGE embedding/rerank models including bge-reranker-v2 and a small Gemma reranker plus training scripts; borrow a self-hosted reranker fine-tuned on your golden pairs. pyserini (~2.2k★, Apache-2.0, pushed Nov 4): reproducible BM25 and vector baselines with built-in eval scripts (`pip install pyserini`); borrow BM25 baseline and standard scoring for the golden set.

## Content

**[qdrant/fastembed](https://github.com/qdrant/fastembed)** runs embedding models and reranking models (cross-encoders) locally on CPU.
- To run it: `pip install fastembed`
- What to borrow: its `TextCrossEncoder` as a cheap local reranker, so dev and CI evals don't need a paid API.
- Maturity: mature, about 3.3k stars, pushed Nov 4, Apache-2.0.
- Best for: Devs.

**[FlagOpen/FlagEmbedding](https://github.com/FlagOpen/FlagEmbedding)** is home to the BGE models for embedding and reranking, including bge-reranker-v2 and a small reranker built on Gemma, plus training scripts.
- What to borrow: a reranker you host yourself and fine-tune on your own golden question and answer pairs.
- Maturity: mature, about 12.3k stars, pushed Oct 27, MIT license.
- Best for: Architects, as a self-hosting option, and Devs.

**[castorini/pyserini](https://github.com/castorini/pyserini)** gives reproducible keyword (BM25) and vector search baselines with built-in eval scripts.
- To run it: `pip install pyserini`
- What to borrow: the BM25 baseline and the standard scoring scripts for your golden set.
- Maturity: mature and academic, about 2.2k stars, pushed Nov 4, Apache-2.0.
- Best for: Devs and Architects.

## Sources

- [fastembed](https://github.com/qdrant/fastembed)
- [FlagEmbedding](https://github.com/FlagOpen/FlagEmbedding)
- [pyserini](https://github.com/castorini/pyserini)