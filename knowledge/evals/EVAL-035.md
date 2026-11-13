# EVAL-035: Eval: cost and latency per correct answer

## Summary

Run the same golden set through 2–4 setups and compare cost per correct answer (not just accuracy)—e.g. search only, wiki only, search+wiki, cheaper model.

## Details

Steps: log correct/tokens/time/dollars; cost÷correct; also p95 latency; plot accuracy vs cost and drop dominated setups; CI fail if cost/correct rises >15% or p95 over budget. Catches setups that only look better by spending 3× tokens, slow cost creep, and cases where a cheaper setup is good enough.

## Sources

- No external source link (in-house technique note).
