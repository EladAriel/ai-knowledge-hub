# EVAL-024: Eval: pass^k (repeat-run consistency)

## Summary

Run each golden question k times (e.g. 5) and count questions answered right on every run, not just once (idea from tau-bench).

## Details

1) Take 30-50 existing questions. 2) Run each 5 times with normal settings. 3) Grade pass/fail with your existing check. 4) Report pass@5 (right at least once) and pass^5 (right every time). 5) List questions in the gap and find where they go wrong: retrieval order, chunks scoring the same, or answer step. Catches unstable retrieval, reranker tie-breaking, answers that change run to run, demos that worked once.

## Sources

- [tau-bench](https://arxiv.org/abs/2406.12045)
