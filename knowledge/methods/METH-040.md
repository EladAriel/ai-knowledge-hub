# METH-040: Raw-RAG baseline beats complex agentic memory

## Summary

Dense retrieval + rerank over raw history ranked first in 6 of 7 settings (LoCoMo, LongMemEval, MEME, MemoryAgentBench).

## Details

Beat the strongest agentic memory system by 0.13-5.53 points; raw chunks cover more evidence incl. relations. Conversation-memory tasks only. Add a raw_rag baseline to the eval harness: any memory or GraphRAG feature must beat it; never let summaries replace the raw chunk store.

## Content

### 3. "Naive RAG Is Stronger Than We Thought": raw-history retrieval beats complex agentic memory
- URL: https://arxiv.org/abs/2610.30755 (2026-10-22)
- What: Raw-RAG (dense retrieval + rerank over raw history) ranked **first in 6 of 7** benchmark-model settings across LoCoMo, LongMemEval, MEME and MemoryAgentBench. It beat the strongest agentic memory system by **0.13-5.53 points**.
- Why: raw chunks cover more of the needed evidence, including relations and dependency paths. Even full access to the transformed memory stores still left an accuracy gap compared with raw evidence. This is a strong confirmation of the recurring "keep raw evidence, make derived memory rebuildable" theme (MemoryTax 10-22, Anti-Persistence 10-21). Limit: tested on conversation-memory tasks only.
- Adopt for:
  - Architects: never let summaries or extracted facts replace the raw chunk store. Derived layers sit on top of raw chunks.
  - Product: before buying or building a "memory" product, ask how it compares with plain retrieval + rerank over raw logs.
  - Devs: add a `raw_rag` baseline to the eval harness. Any memory or GraphRAG feature must beat it.

## Sources

- [Naive RAG Is Stronger Than …](https://arxiv.org/abs/2610.30755)