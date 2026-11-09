# TOOL-019: Repos: gbrain, LanceDB, ParadeDB

## Summary

Markdown-first company brain with public evals; embedded versioned vector store; BM25+vector inside Postgres.

## Details

garrytan/gbrain (31.2k, MIT): Markdown source of truth, Postgres/PGLite hybrid index; borrow gbrain-evals (pre-registered; 0/100 finance-only docs leaked, forgetting checks, recall per scope). lancedb/lancedb (11.8k, Apache-2.0): automatic table versions as cheap rollback after bad re-embed. paradedb/paradedb (9.4k, AGPL-3.0): keyword, vectors, app data and permission columns in one transaction so index can't drift from permissions.

## Content

**[garrytan/gbrain](https://github.com/garrytan/gbrain)** is agent memory and a "company brain" built on Markdown files as the source of truth. The search index runs on Postgres or embedded PGLite and combines keyword search, vectors and reranking, plus typed links between files.
- What to borrow: its public eval suite, [gbrain-evals](https://github.com/garrytan/gbrain-evals). The tests were registered in advance. It includes permission-leak results (0 of 100 finance-only docs leaked), checks that forgotten data is really gone, and recall numbers per scope.
- Maturity: 31.2k stars, 4.7k forks, MIT, pushed today. Its author runs it in production, but it's very opinionated. Install with `bun install -g github:garrytan/gbrain`.
- Best for: Devs and Architects.

**[lancedb/lancedb](https://github.com/lancedb/lancedb)** is an embedded store for vectors, full-text search and SQL, built on the Lance columnar format. It versions tables automatically, and has Python, TypeScript and Rust SDKs.
- What to borrow: table versions as a cheap rollback after a bad re-embed or reindex, and local development with no server.
- Maturity: 11.8k stars, Apache-2.0, pushed today. It's used in production and has a cloud offering.
- Best for: Devs.

**[paradedb/paradedb](https://github.com/paradedb/paradedb)** is a Postgres extension that adds BM25 keyword search, vector and hybrid search, filters and facets, all inside one transactional database.
- What to borrow: keeping keyword search, vectors and app data, including permission columns, in one transaction, so the index can't drift out of sync with permissions.
- Maturity: 9.4k stars, pushed today, installs with Docker. The license is AGPL-3.0, so check with legal before building it into a product.
- Best for: Architects.

## Sources

- [gbrain](https://github.com/garrytan/gbrain)
- [gbrain-evals](https://github.com/garrytan/gbrain-evals)
- [lancedb](https://github.com/lancedb/lancedb)
- [paradedb](https://github.com/paradedb/paradedb)