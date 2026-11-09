# TOOL-007: Repos: WeKnora, rank_llm, headroom

## Summary

Open-source knowledge platform; reproducible LLM reranking toolkit; reversible context compression proxy.

## Details

Tencent/WeKnora (~34.5k, MIT): hybrid search with pluggable rerankers, 4-level workspace roles with audit, per-workspace MCP endpoint, Langfuse tracing per stage. castorini/rank_llm (~660, Apache-2.0): one harness to compare rerankers on your own queries. headroomlabs-ai/headroom (~75.6k, Apache-2.0): drop-in proxy (headroom proxy --port 8787) compressing tool outputs/logs/RAG chunks reversibly; model fetches originals via headroom_retrieve; savings are self-reported.

## Content

**[Tencent/WeKnora](https://github.com/Tencent/WeKnora)** is a full open-source knowledge platform covering RAG, an agent, and a wiki that maintains itself.
- Maturity: about 34.5k stars and 4.6k forks. v0.8.3 came out Oct 14, the README says it's MIT licensed, and it starts with `docker compose up -d`.
- What to borrow:
  - hybrid search with pluggable rerankers (TEI, Cohere, Pinecone and others), including reranking that handles images
  - four levels of workspace roles, with audit logs
  - a separate MCP endpoint per workspace, each with its own token and knowledge-base scope
  - Langfuse tracing of each pipeline stage
- Best for: Architects, as a working reference design to compare against your own.

**[castorini/rank_llm](https://github.com/castorini/rank_llm)** is a Python toolkit for reproducible reranking, mostly with LLMs that reorder a whole list at once. It's from the same Waterloo group as insight 3.
- Maturity: about 660 stars, Apache-2.0, with commits as recent as today. It installs with `uv pip install rank-llm`, and custom prompt templates live in YAML.
- What to borrow: one harness that compares several rerankers on your own queries before you commit to one.
- Best for: Devs.

**[headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom)** compresses tool outputs, logs and RAG chunks before they reach the LLM.
- Maturity: about 75.6k stars, Apache-2.0. v0.41.0 came out Oct 14, and you install it with `pip install "headroom-ai[all]"` or the npm SDK.
- What to borrow: it runs as a drop-in proxy (`headroom proxy --port 8787`), and the compression is reversible. The original text stays cached, and the model can fetch it with a `headroom_retrieve` tool. That directly targets Kapa's finding that agentic retrievers send far too many tokens.
- Caveat: the token savings are the project's own numbers, so measure them on your traffic.
- Best for: Devs, with Product tracking the cost savings.

## Sources

- [WeKnora](https://github.com/Tencent/WeKnora)
- [rank_llm](https://github.com/castorini/rank_llm)
- [headroom](https://github.com/headroomlabs-ai/headroom)