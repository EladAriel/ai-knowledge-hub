# PIPE-017: Pipeline: ingestion contracts and trust tiers

## Summary

source API -> managed login/proxy -> connector emits standard record -> schema check (accept/freeze/quarantine) -> raw ….

## Details

Uniform record: doc_id, source, version, updated_at, change_type, acl, authority_tier, raw_uri. Unknown fields/types go to a quarantine table. Keep raw copy; parsed versions rebuildable. ….

## Sources

- [practitioner guide](https://cloudsoftsol.com/blog/data-pipelines-for-rag/)
- [Executable Schema Contracts](https://arxiv.org/abs/2606.05415)
