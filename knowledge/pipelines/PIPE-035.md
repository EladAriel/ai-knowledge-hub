# PIPE-035: Pipeline: ingestion and connectors — make every sync safe to repeat

## Summary

Ingestion angle (Nov 20): make every sync safe to repeat. Give each item a stable ID, such as gh-issue-123, plus a fingerprint of its content. Re-embed an item only when its fingerprint changes. Record deleted items as deleted instead of silently dropping them. That way a repeated sync costs almost nothing and never leaves deleted docs lingering in the index.

## Details

This differs from earlier ingestion angles (PIPE-008, PIPE-017, PIPE-023), which were about connector contracts, trust tiers, or event-driven page hashes and a completion marker. Today's practice is the idempotent repeat: a stable ID, a content fingerprint, and a deletion record.

Who owns it: Architects define the ID, fingerprint and deletion-record scheme for every connector. Devs implement re-embed-on-change and keep deleted items marked as deleted. Product checks that a repeated sync does not change the document count.

See also EVAL-044 (re-sync churn test) and EVAL-030 (duplicate crowding and repeat syncs).

## Sources

- [EVAL-044: re-sync churn test](../evals/EVAL-044.md)
- [EVAL-030: duplicate crowding and repeat syncs](../evals/EVAL-030.md)
