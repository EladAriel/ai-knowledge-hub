# PIPE-039: Pipeline: permissions — every side path follows the same rules as search

## Summary

Permissions angle (Nov 24): every side path follows the same rules as search. The cache, agent memory, logs and traces all use the user's permission set as the key. If a chunk's access list is missing or stale, deny access. Check permissions again right before building the context.

## Details

This differs from earlier permissions angles (PIPE-003, PIPE-012, PIPE-021, PIPE-030), which were about filtering in retrieval itself. Today's practice is the side paths: cache, memory, logs and traces, plus a second check just before the context is built.

Who owns it: Architects require the same permission key on every side path, and deny access when a chunk's access list is missing or stale. Devs key the cache, memory, logs and traces by the user's permission set, and re-check before building the context. Product reviews leak tests that go through those side paths.

See also METH-206 (permission-aware RAG demo), METH-207 (safe caching), METH-208 (memory scopes), and EVAL-047 (cross-user side-path leak test).

## Sources

- [Permission-aware RAG (METH-206)](https://wittyprogramming.dev/articles/permission-aware-rag/)
- [Safe caching, EMNLP 2026 Industry (METH-207)](https://aclanthology.org/2026.emnlp-industry.75/)
- [Shared agent memory needs scopes (METH-208)](https://arxiv.org/abs/2611.10439)
