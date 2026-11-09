# TOOL-022: Repos: haiku.rag, sentence-transformers v6.2, Infinity

## Summary

Local agentic RAG with swappable rerankers; fine-tune your own cross-encoder reranker; self-hosted embeddings/rerank server.

## Content

**[haiku.rag](https://github.com/ggozad/haiku.rag)** is local agentic RAG. It parses with Docling, stores data in LanceDB, and combines vector and full-text search. It also has swappable rerankers (cross-encoders, Cohere, Jina and more), citations down to the page and heading, an MCP server, and an ingester with a job queue.
- What to borrow: the reranker plugin design, and the `haiku-rag doctor` health checks.
- Maturity: 639 stars, MIT, pushed Oct 26, with tests, coverage and [docs](https://ggozad.github.io/haiku.rag/) that include a quickstart.
- Best for: Devs, and Product for a quick demo on real documents.

**[sentence-transformers](https://github.com/huggingface/sentence-transformers)** ([v6.2](https://github.com/huggingface/sentence-transformers/releases/tag/v6.2.0), Oct 21) is the standard library for fine-tuning your own reranker on company data.
- What to borrow: the [CrossEncoder training guide](https://sbert.net/docs/cross_encoder/training_overview.html), and `CrossEncoderRerankingEvaluator` for CI. v6.2 also adds `CrossEncoder.merge` for combining fine-tuned models.
- Maturity: 19.2k stars, Apache-2.0.
- Best for: Devs.

**[Infinity](https://github.com/michaelfeil/infinity)** is a self-hosted server for embeddings, reranking (through `/rerank`) and sparse keyword-style vectors (SPLADE). Version 3 is a new Rust server from October 2026 that starts with one Docker command.
- License warning: v3 uses a custom "Infinity Restricted MIT License" that bans use on 25 listed providers. Older packages, including the Python v2 server, keep their own licenses. Read `LICENSING.md` before adopting it.
- Maturity: 3k stars, pushed today.
- Best for: Architects planning reranking inside their own network.

## Sources

- [haiku.rag](https://github.com/ggozad/haiku.rag)
- [sentence-transformers](https://github.com/huggingface/sentence-transformers)
- [infinity](https://github.com/michaelfeil/infinity)
- [docs](https://ggozad.github.io/haiku.rag/)
- [v6.2](https://github.com/huggingface/sentence-transformers/releases/tag/v6.2.0)
- [CrossEncoder training guide](https://sbert.net/docs/cross_encoder/training_overview.html)
