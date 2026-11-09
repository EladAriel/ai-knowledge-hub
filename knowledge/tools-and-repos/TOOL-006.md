# TOOL-006: Repos: Onyx, Graphiti, Hindsight

## Summary

Enterprise search with per-connector permission sync; temporal knowledge graph for memory; Postgres agent memory.

## Details

onyx-dot-app/onyx (~32.5k stars): borrow per-connector permission-sync layout and post_query_censoring.py (ee folder, enterprise license: copy design, not code). getzep/graphiti (~31.8k, Apache-2.0): facts as edges with validity windows, old facts invalidated not deleted ('what was true on date X'). vectorize-io/hindsight (~50.6k, MIT, v1.0.0): retain/recall/reflect API, memory banks per team, Postgres single store.

## Content

- **[onyx-dot-app/onyx](https://github.com/onyx-dot-app/onyx)**: open-source enterprise search and chat. Connectors ingest content plus metadata and permissions.
  - **Borrow:** the per-connector permission-sync layout ([`backend/ee/onyx/external_permissions`](https://github.com/onyx-dot-app/onyx/tree/main/backend/ee/onyx/external_permissions): Slack, Confluence, Google Drive, SharePoint, Jira, Salesforce, etc.) and `post_query_censoring.py`, which filters at query time for sources that cannot be pre-synced.
  - **Caveat:** that code is in the `ee` folder under the Onyx Enterprise License. Copy the design, not the code. The Community Edition is MIT.
  - **Maturity:** ~32.5k stars, 4.6k forks, last commit Oct 17, 2026. One-line install script or Docker/K8s/Helm.
  - **Best for:** Architects (a reference architecture for connectors plus ACLs).

- **[getzep/graphiti](https://github.com/getzep/graphiti)**: temporal knowledge graph (a graph that tracks when facts were true) for agent memory.
  - **Borrow:** facts as edges with validity windows. When something changes, the old fact is marked invalid, not deleted, so you can ask "what was true on date X". This directly answers the FEB-30 failure mode.
  - **Maturity:** ~31.8k stars, Apache-2.0, last commit Oct 15, 2026 (v0.31.1). `pip install graphiti-core` with Neo4j, FalkorDB (Docker one-liner), or Neptune.
  - **Best for:** Architects and Devs.

- **[vectorize-io/hindsight](https://github.com/vectorize-io/hindsight)**: agent memory on Postgres with a `retain` / `recall` / `reflect` API, and Python and TypeScript clients.
  - **Borrow:** memory "banks" (separate namespaces, e.g. per team), Postgres as a single store with transactions, backups, and access control, plus a live benchmark page.
  - **Maturity:** ~50.6k stars, MIT, v1.0.0 released Oct 13, 2026, last commit Oct 16. Docker run, pip, or Helm. LongMemEval SOTA is the vendor's claim, which it says Virginia Tech reproduced.
  - **Best for:** Devs (fastest local setup), then Product (quick prototypes).

## Sources

- [onyx](https://github.com/onyx-dot-app/onyx)
- [graphiti](https://github.com/getzep/graphiti)
- [hindsight](https://github.com/vectorize-io/hindsight)
- [`backend/ee/onyx/external_permissions`](https://github.com/onyx-dot-app/onyx/tree/main/backend/ee/onyx/external_permissions)