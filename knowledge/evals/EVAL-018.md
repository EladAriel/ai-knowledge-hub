# EVAL-018: Eval: filtered index recall audit

## Summary

Compare index results with exact brute-force top results, separately per filter scope.

## Details

1) 200 real queries. 2) Exact top results via full scan/numpy. 3) Same query through the production index per scope: no filter, one tenant, 10% ACL slice, one source. 4) recall@10/@50, short-result rate, p50 latency. 5) Fail CI if any scope drops below target (e.g. 0.95). Catches silent misses under ACL filters, bad search settings, reindex/model regressions, missing stats.

## Content

## Simple eval technique: filtered index recall audit

**What it is:** you compare what your index returns against the true top results from an exact, brute-force search. You check each filter scope separately.

**Steps (under a day):**
1. Take 200 real queries.
2. For each query, find the exact top results with a full scan, or with numpy over the vectors.
3. Run the same query through the production index in each scope: no filter, one tenant, a 10% ACL slice and one source.
4. Report recall@10 and recall@50, how often fewer results come back than you asked for, and median (p50) latency.
5. Fail CI if any scope drops below its target, for example 0.95.

**What it catches:** silent misses under ACL filters, bad index search settings, regressions after a reindex or model change, and missing database statistics.

**Who runs it:** Devs build it and run it in CI. Architects set the target for each scope and decide on partitioning. Product picks which scopes matter, meaning which teams and spaces.