# PIPE-017: Pipeline: ingestion contracts and trust tiers

## Summary

source API -> managed login/proxy -> connector emits standard record -> schema check (accept/freeze/quarantine) -> raw store -> lineage event -> parse and index.

## Details

Uniform record: doc_id, source, version, updated_at, change_type, acl, authority_tier, raw_uri. Unknown fields/types go to a quarantine table. Keep raw copy; parsed versions rebuildable. One schema as shared contract for KG building and routing (Executable Schema Contracts). Tag trust level at ingestion: system of record > wiki > chat. Devs: connector template with contract tests; CI fails on unknown fields.

## Content

## Pipeline pattern of the day: ingestion and connectors, part 2 (contracts and trust)

source API -> managed login and proxy -> connector emits a standard record -> schema check (accept the change, freeze, or quarantine) -> raw store -> lineage event -> parse and index

- **Every connector emits the same record format:** `doc_id, source, version, updated_at, change_type, acl, authority_tier, raw_uri` ([practitioner guide](https://cloudsoftsol.com/blog/data-pipelines-for-rag/)).
- **Check the shape at the gate.** Unknown fields or data types go to a quarantine table for review, not straight into the index, as dlt's contracts do.
- **Keep the raw copy,** and treat parsed versions as something you can rebuild (the log-parsing paper).
- **Use one schema as a shared contract** for both building the knowledge graph and routing questions ([Executable Schema Contracts](https://arxiv.org/abs/2606.05415)).
- **Tag each source's trust level when it comes in.** The official system of record ranks above the wiki, and the wiki ranks above chat (the Era benchmark).
- **Who owns it:**
  - *Architects* own the record format, the trust tiers and the quarantine policy.
  - *Product* owns which source is the truth for each question type, and the order sources get added.
  - *Devs* own a connector template with contract tests, plus a CI check that fails when an unknown field appears.

## Sources

- [practitioner guide](https://cloudsoftsol.com/blog/data-pipelines-for-rag/)
- [Executable Schema Contracts](https://arxiv.org/abs/2606.05415)