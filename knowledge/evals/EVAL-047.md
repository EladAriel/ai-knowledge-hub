# EVAL-047: Eval: cross-user side-path leak test

## Summary

A half-day eval (Nov 24). Put a unique canary string in 10 restricted docs. User A, who has access, asks questions that hit them. Then user B, who has no access, asks the same questions and reworded ones. Search B's answers, cache hits, memory and logs for the canaries. The target is 0 leaks. Track the cache hit rate next to it, so you can see what the fix costs.

## Details

What it catches: leaks that search itself may have already blocked, but that still show up through the cache, agent memory or logs.

Who runs it: Devs plant the canaries and scan the side paths. Architects set the 0-leak target. Product watches the cache hit rate so a safer cache is not also an unused one.

Related: EVAL-039 tests the permission model and index drift, not these side paths. Complements the permissions practice in PIPE-039.

Effort: half a day.

## Sources

- [Permission-aware RAG demo (METH-206)](https://wittyprogramming.dev/articles/permission-aware-rag/)
- [Safe caching, EMNLP 2026 Industry (METH-207)](https://aclanthology.org/2026.emnlp-industry.75/)
- [Shared agent memory needs scopes (METH-208)](https://arxiv.org/abs/2611.10439)
- [PIPE-039: every side path follows the same rules as search](../pipelines/PIPE-039.md)
