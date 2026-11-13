# TOOL-040: Repos: microsoft/multi-modal-rag-with-colpali, bgts-context-engine, context-mode

## Summary

Three repos from the Nov 9 retrieval brief: Microsoft's open ColPali RAG sample PULSAR was built on, bgts-context-engine (deterministic code graph for coding agents, LLM-free ranking), and context-mode (hooks that store tool output in a search index instead of the prompt; Elastic 2.0 license).

## Details

microsoft/multi-modal-rag-with-colpali: event-triggered ingestion on Azure, hash-based resume, ColQwen3 on vLLM, Qdrant, deployment files. Borrow the ingestion worker and the shared vector format used by indexing and search. MIT, 27 stars, pushed Nov 6; README says it isn't production-ready. For Architects (reference design) and Devs.
bgts-ai-org/bgts-context-engine: code graph for coding agents (functions, calls, routes, cross-language links); same task on the same code always gets the same results. Self-reported benchmark on 600 PRs: 60-67% lower cost, 88-90% fewer tool calls, about the same file-finding ability. Borrow LLM-free ranking plus a small model that can only remove candidates, never add them. MIT, 179 stars, pushed Nov 2. For Devs.
mksglu/context-mode: repo behind insight #3, Context Mode 2.0 (METH-113) (33.7k stars, active). Borrow hooks that store tool output in a search index instead of pasting it into the prompt. License warning: Elastic 2.0, source-available, not open source; check terms before building into a product. For Devs.

## Content

## Repos to adopt

**[microsoft/multi-modal-rag-with-colpali](https://github.com/microsoft/multi-modal-rag-with-colpali)** is the open Microsoft sample PULSAR was built on.
- What it does: ingestion triggered by events on Azure, with resume based on hashes, ColQwen3 served on vLLM, Qdrant for vectors, and deployment files.
- What to borrow: the ingestion worker, and the shared vector format that indexing and search both use.
- Maturity: MIT license, 27 stars, pushed Nov 6. The README says it isn't production-ready.
- Best for: Architects as a reference design, and Devs.

**[bgts-ai-org/bgts-context-engine](https://github.com/bgts-ai-org/bgts-context-engine)** builds a graph of code for coding agents, covering functions, calls, routes and links between languages. The same task on the same code always gets the same results.
- Results: their own [benchmark post](https://bgts.com/blog/bgts-context-engine/) on 600 pull requests reports 60–67% lower cost and 88–90% fewer tool calls, with about the same ability to find the right files. These numbers are self-reported.
- What to borrow: ranking with no LLM involved, plus a small model that can only remove candidates, never add them.
- Maturity: MIT license, 179 stars, pushed Nov 2.
- Best for: Devs. It's mostly code-graph navigation, like an IDE's code intelligence, with good ranking.

**[mksglu/context-mode](https://github.com/mksglu/context-mode)** is the repo behind insight 3 (Context Mode 2.0, METH-113), with 33.7k stars and active today.
- What to borrow: hooks that store tool output in a search index instead of pasting it into the prompt.
- License warning: it's Elastic 2.0. You can read the source, but it isn't open source, so check the terms before building it into a product.
- Best for: Devs.

## Sources

- [multi-modal-rag-with-colpali](https://github.com/microsoft/multi-modal-rag-with-colpali)
- [bgts-context-engine](https://github.com/bgts-ai-org/bgts-context-engine)
- [bgts benchmark post](https://bgts.com/blog/bgts-context-engine/)
- [context-mode](https://github.com/mksglu/context-mode)
