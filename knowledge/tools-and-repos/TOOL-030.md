# TOOL-030: Repos: dlt, Nango, OpenLineage

## Summary

Typed loading with schema contracts; managed OAuth/proxy/syncs for 1,000+ APIs; lineage events per run.

## Details

dlt-hub/dlt (~6k, Apache-2.0): schema contracts evolve/freeze/discard, incremental('updated_at'), merge on primary key. NangoHQ/nango (~13k, Elastic License 2.0): OAuth, token refresh, rate limits, TypeScript sync functions for RAG. OpenLineage (~2.7k, Apache-2.0, Marquez): one lineage event per ingestion run so any chunk traces to source, job, version.

## Content

**[dlt-hub/dlt](https://github.com/dlt-hub/dlt)** is a Python library, not a platform, for loading APIs and databases into typed tables.
- What to borrow:
  - Its [schema contracts](https://dlthub.com/docs/general-usage/schema-contracts), which decide what happens when a table, column or data type changes. "Evolve" accepts the change, "freeze" rejects it and "discard" drops it.
  - `incremental("updated_at")`, which loads only rows changed since the last run.
  - Merging on a primary key, so updates replace old rows instead of duplicating them.
- Maturity: mature. About 6.0k stars, pushed today, Apache-2.0, with a `pip install dlt` quick start.
- Best for: Devs and Architects.

**[NangoHQ/nango](https://github.com/NangoHQ/nango)** handles login (OAuth), token refresh and request proxying for over 1,000 APIs. It also has [sync functions](https://nango.dev/docs/guides/functions/syncs/sync-functions) that keep data in sync for RAG pipelines and webhooks, written in TypeScript.
- What to borrow: let it handle login and rate limits, so each connector doesn't have to.
- Maturity: about 13k stars, actively developed.
- License: Elastic License 2.0, so you can't offer it as a hosted service, and the free self-hosted version has fewer features.
- Best for: Devs working in TypeScript, and Product, since new sources get added faster.

**[OpenLineage/OpenLineage](https://github.com/OpenLineage/OpenLineage)** is an open standard for recording which job read and wrote which datasets in each run. It has Airflow, Spark and dbt integrations, and Marquez is its reference server.
- What to borrow: emit one lineage event per ingestion run, so any chunk can be traced back to its source, job and version.
- Maturity: mature. About 2.7k stars, Apache-2.0, actively developed.
- Best for: Architects.

## Sources

- [dlt](https://github.com/dlt-hub/dlt)
- [nango](https://github.com/NangoHQ/nango)
- [OpenLineage](https://github.com/OpenLineage/OpenLineage)
- [schema contracts](https://dlthub.com/docs/general-usage/schema-contracts)
- [sync functions](https://nango.dev/docs/guides/functions/syncs/sync-functions)