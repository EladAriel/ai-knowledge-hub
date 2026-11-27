# METH-207: Safe caching: a cache can leak even when retrieval doesn't

## Summary

Normal RAG caches gave back stale or unauthorized evidence in 3.4–9.8% of reuses. Even with a time-to-live expiry, that was still 0.3–8.2%. The fix is to cache evidence chunks, not final answers. Before each reuse, check two things: is this user allowed to see it, and is the source document still current? On the authors' internal role-based workload, latency dropped 22% and retrieval cost 34%, with zero bad reuses. These are internal numbers, and no code was found. Next step: if you cache answers today, switch to caching chunks and check access on every hit. For: architects.

## Details

Reported Nov 24. Complements today's permissions practice in PIPE-039 and the leak test in EVAL-047.

## Sources

- [Safe caching (EMNLP 2026 Industry)](https://aclanthology.org/2026.emnlp-industry.75/)
