# PIPE-008: Pipeline: ingestion and connectors

## Summary

change webhook (hint) -> delta pull (source of truth) -> fetch content, ACL, metadata -> stable doc ID + content hash ….

## Details

Delta tokens expire (410 Gone = full resync); changes can repeat; deletes arrive as @removed, so writes must be idempotent. Check 'what changed' and 'does it still exist' separately (Onyx slim connectors list IDs to find ….

## Sources

- [Graph delta query](https://learn.microsoft.com/en-us/graph/delta-query-overview)
- [Onyx connectors](https://github.com/onyx-dot-app/onyx/blob/main/backend/onyx/connectors/README.md)
