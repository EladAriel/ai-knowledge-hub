# TOOL-047: Repos: authzed agentic-rag-authorization, knowledge-intelligence, ash-ding/MAPE

## Summary

The official SpiceDB RAG example that checks each chunk in a node the agent can't skip; a multi-tenant permission-aware RAG platform; and the code for evolving agent memory designs.

## Details

authzed/examples agentic-rag-authorization is the code behind Elastic's post on RAG with SpiceDB permissions (Nov 11). Elasticsearch kNN, then a deterministic LangGraph node checks each chunk against SpiceDB, then the LLM (Mistral). It runs with Docker Compose and includes tests. Borrow: a permission step the agent can't skip; any error means access is denied; sharing or removing access is one change in SpiceDB, with no re-indexing. Maturity: an official vendor example with 68 stars and 13 forks across the repo, Apache-2.0, last updated Oct 26. It's a demo, so SpiceDB keeps its data in memory only. Best for Devs. This is a different example from the Oct 26 SpiceDB workshop in TOOL-021 (that one pre-filters viewable IDs before Qdrant). Safiullah-Rahu/knowledge-intelligence is an enterprise RAG platform for multiple customers that respects permissions, built with FastAPI, Postgres with pgvector, and Next.js. Borrow: Postgres row-level security on every customer table; grants that expire, where a deny beats any allow; tests that check no data leaks between customers; combined keyword and vector search over only the documents the user may see; an add-only audit log. Maturity: 342 stars and 43 forks, MIT, last pushed Nov 2, with 164 backend tests and a doc on evaluating its RAG. It has one maintainer, so use it as a reference design rather than a dependency. Best for Architects. ash-ding/MAPE is the code for Discovering Agent Memory Designs via Program Evolution (arXiv 2611.17068); see METH-161 for the paper. Borrow: the build, retrieve and compose split as your memory interface, plus the setup for comparing memory systems side by side. Maturity: research code with 2 stars, Apache-2.0, last pushed Nov 9, under review. Best for Devs.

## Sources

- [authzed/examples agentic-rag-authorization](https://github.com/authzed/examples/tree/main/agentic-rag-authorization)
- [Elastic: RAG with SpiceDB](https://www.elastic.co/search-labs/blog/fine-grained-authorization-elasticsearch-rag-spicedb)
- [knowledge-intelligence](https://github.com/Safiullah-Rahu/knowledge-intelligence)
- [ash-ding/MAPE](https://github.com/ash-ding/MAPE)
