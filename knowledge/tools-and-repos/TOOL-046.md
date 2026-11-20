# TOOL-046: Repos: alibaba/zvec, RaBitQ-Library, xerrors/Yuxi

## Summary

An in-process vector database with no separate server, the official library for the RaBitQ vector-compression method, and a self-hosted knowledge-agent platform for multiple teams.

## Details

alibaba/zvec is a vector database that runs inside your app, with no separate server. It does keyword search, vector search and both combined, plus a write log so data survives a crash. Borrow: combined search and filters in one query, and local development with no infrastructure. Maturity: about 16.2k stars, Apache-2.0, released v0.8.1 on Nov 6, has CI. Best for Devs, for local work and tests. VectorDB-NTU/RaBitQ-Library is the official library for RaBitQ, a vector compression method with a known worst-case error. It shrinks vectors to 1–9 bits per number. Install: pip install rabitqlib. Borrow: use it to test how well your own embeddings hold up at different sizes. Maturity: 297 stars, Apache-2.0, commits on Nov 12, and zvec uses it. Best for Architects and Devs planning capacity. xerrors/Yuxi is a self-hosted knowledge-agent platform for multiple teams. It searches over documents with Milvus, a knowledge graph in Neo4j, LangGraph agents, MCP and skills, and a sandbox. Access can be set per user, per department, or shared. Borrow: that permission model, and its Docker setup. Maturity: about 7.7k stars, MIT, v0.8.0 released Nov 10 (fresh installs only). The main README is in Chinese, with an English version too. Best for Architects, as a reference design.

## Sources

- [alibaba/zvec](https://github.com/alibaba/zvec)
- [RaBitQ-Library](https://github.com/VectorDB-NTU/RaBitQ-Library)
- [xerrors/Yuxi](https://github.com/xerrors/Yuxi)
