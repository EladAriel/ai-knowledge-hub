# EVAL-029: Eval: context order test (lost-in-the-middle sensitivity to chunk position)

## Summary

Check whether the answer changes depending on where the right chunk sits in the context. Models tend to use facts at the start and end better than in the middle (Lost in the Middle).

## Details

Steps (under a day): 1) Take 30–50 golden questions, each with a known correct chunk. 2) Build a context with the correct chunk plus 9 other retrieved chunks. 3) Run four versions: correct chunk first / middle / last / reranker's order reversed. 4) Score each answer right or wrong (exact match or yes/no LLM judge). 5) Report accuracy per position and the gap between best and worst; fail CI if the gap is over about 10 points. What it catches: whether the answer model depends on the reranker's order (best-first, both ends, or fewer chunks), and regressions after a model swap.

## Sources

- (no public source link recorded)
