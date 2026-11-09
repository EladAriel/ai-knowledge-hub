# EVAL-004: Eval: golden question set + retrieval recall@k (with negative ACL cases)

## Summary

Fixed real questions labeled with gold doc IDs; measure recall@5/@10, MRR and leak count per user in CI.

## Details

1) 50-100 real questions from Slack/tickets/search logs. 2) Gold doc IDs, expert spot-check ~20%. 3) 10-20 negative ACL cases (user, question, forbidden doc). 4) golden.jsonl {q,user,gold_ids,forbidden_ids}. ….

## Sources

- (no public source link recorded)
