# PIPE-008: Pipeline: ingestion and connectors

## Summary

change webhook (hint) -> delta pull (source of truth) -> fetch content, ACL, metadata -> stable doc ID + content hash -> idempotent upsert or tombstone -> reconcile.

## Details

Delta tokens expire (410 Gone = full resync); changes can repeat; deletes arrive as @removed, so writes must be idempotent. Check 'what changed' and 'does it still exist' separately (Onyx slim connectors list IDs to find deletes). updated_at sync has blind spots. Permission changes lag content (SharePoint parent-folder ACL needs explicit resync); deny when a check can't be made. Devs: stable IDs, tombstones, nightly reconcile, indexed/deleted events, replay recorded webhooks/deltas in tests.

## Content

## Pipeline pattern of the day: ingestion and connectors

change webhook (a hint) -> delta pull (the source of truth) -> fetch content, access list (ACL) and metadata -> stable doc ID plus content hash -> idempotent upsert, or a \...ecycle notifications](https://learn.microsoft.com/en-us/graph/change-notifications-lifecycle-events)).
- **Delta tokens expire, and changes can repeat.** A `410 Gone` response means you need a full resync. The same change can arrive twice, and deletes arrive as `@removed`, so writes must be safe to repeat ([Graph delta query](https://learn.microsoft.com/en-us/graph/delta-query-overview)).
- **Check "what changed" and "does it still exist" separately.** Onyx uses polling connectors for updates, and lightweight "slim" connectors that only list IDs to find deleted docs ([Onyx connectors](https://github.com/onyx-dot-app/onyx/blob/main/backend/onyx/connectors/README.md)).
- **Sync based on an "updated at" field has blind spots.** Records can arrive more than once, edits that don't change that field are missed, and you only see deletes from sources that report them ([Airbyte incremental sync](https://docs.airbyte.com/platform/using-airbyte/core-concepts/sync-modes/incremental-append-deduped)).
- **Permission changes reach the index later than content changes.** In SharePoint, an ACL change on a parent folder needs an explicit resync ([SharePoint ACL ingestion](https://learn.microsoft.com/en-us/azure/search/search-indexer-sharepoint-access-control-lists)). At query time, deny access when a check can't be made ([Azure query-time enforcement](https://learn.microsoft.com/en-us/azure/search/search-query-access-control-rbac-enforcement)).
- **Who owns it:**
  - *Architects* own a contract for each source: how changes are signalled, how ACLs are fetched, how IDs are listed and how deletes work. They also own the freshness and permission-lag targets.
  - *Product* sets freshness targets based on how critical each source is, and makes "revoked access disappears within X minutes" a launch requirement.
  - *Devs* build stable IDs, deleted markers, a nightly reconcile job and indexed/deleted events. They test connectors by replaying recorded webhooks and deltas."}

## Sources

- [Graph delta query](https://learn.microsoft.com/en-us/graph/delta-query-overview)
- [Onyx connectors](https://github.com/onyx-dot-app/onyx/blob/main/backend/onyx/connectors/README.md)
- [Airbyte incremental sync](https://docs.airbyte.com/platform/using-airbyte/core-concepts/sync-modes/incremental-append-deduped)
- [SharePoint ACL ingestion](https://learn.microsoft.com/en-us/azure/search/search-indexer-sharepoint-access-control-lists)
- [Azure query-time enforcement](https://learn.microsoft.com/en-us/azure/search/search-query-access-control-rbac-enforcement)