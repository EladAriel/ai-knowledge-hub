# TOOL-012: Repos: Quivr V2, CocoIndex, Azure agent-app-ingestion

## Summary

Durable ingestion service; incremental pipeline engine; ingestion with delete jobs and confirmed audit events.

## Content

**[The-Vibe-Company/quivr](https://github.com/The-Vibe-Company/quivr)** is Quivr V2. It's a near-total pivot from the 2023 "second brain" app into a durable ingestion service built on Go, Postgres, Temporal and Weaviate.
- What to borrow:
  - An idempotency key on every write, so retries don't create duplicates.
  - Corrections saved as new versions instead of overwrites.
  - Keyword search that works before embeddings finish.
  - An index you can rebuild from scratch.
  - Permissions re-checked on every search hit.
  - Real errors instead of empty "success" results.
- Maturity: 39.6k stars, MIT, last pushed Oct 21. The README says not to run it in production yet.
- Best for: Architects and Devs.

**[cocoindex-io/cocoindex](https://github.com/cocoindex-io/cocoindex)** is an incremental pipeline engine with a Rust core and a Python API.
- What to borrow: it reprocesses a file only when the file or your pipeline code changes, removes rows for deleted files, and re-embeds only the files that changed.
- Maturity: 11.7k stars, Apache-2.0, pushed today, with a runnable quickstart.
- Best for: Devs.

**[Azure/agent-app-ingestion](https://github.com/Azure/agent-app-ingestion)** is Microsoft's ingestion service for Blob storage, SharePoint and Azure AI Search.
- What to borrow: separate jobs for indexing and for deleting, plus audit events (such as `document.deleted`) that fire only after the search index confirms the write. Its [runtime guide](https://github.com/Azure/agent-app-ingestion/blob/main/docs/runtime.md) warns that a passing health check doesn't prove documents are being indexed.
- Maturity: 188 stars, MIT, pushed Oct 20. It needs Azure infrastructure.
- Best for: Architects.

## Sources

- [quivr](https://github.com/The-Vibe-Company/quivr)
- [cocoindex](https://github.com/cocoindex-io/cocoindex)
- [agent-app-ingestion](https://github.com/Azure/agent-app-ingestion)
- [runtime guide](https://github.com/Azure/agent-app-ingestion/blob/main/docs/runtime.md)
