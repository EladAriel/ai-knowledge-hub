# EVAL-018: Eval: filtered index recall audit

## Summary

Compare index results with exact brute-force top results, separately per filter scope.

## Details

1) 200 real queries. 2) Exact top results via full scan/numpy. 3) Same query through the production index per scope: no filter, one tenant, 10% ACL slice, one source. 4) recall@10/@50, short-result rate, p50 latency. ….

## Sources

- (no public source link recorded)
