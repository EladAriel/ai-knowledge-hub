# EVAL-029: Eval: context order test (lost-in-the-middle sensitivity to chunk position)

## Summary

Check whether the answer changes depending on where the right chunk sits in the context. Models tend to use facts at the start and end better than in the middle (Lost in the Middle).

## Details

Steps (under a day): 1) Take 30–50 golden questions, each with a known correct chunk. 2) Build a context with the correct chunk plus 9 other retrieved chunks. 3) Run four versions: correct chunk first / middle / last / reranker's order reversed. 4) Score each answer right or wrong (exact match or yes/no LLM judge). 5) Report accuracy per position and the gap between best and worst; fail CI if the gap is over about 10 points. What it catches: whether the answer model depends on the reranker's order (best-first, both ends, or fewer chunks), and regressions after a model swap. Who runs it: Devs in CI; Product sets the acceptable gap; Architects set the ordering rule in the retrieval contract.

## Content

## Simple eval technique: the context order test

2. Build a context with the correct chunk plus 9 other retrieved chunks.
3. Run four versions:
   - the correct chunk first
   - the correct chunk in the middle
   - the correct chunk last
   - the reranker's order reversed
4. Score each answer right or wrong, by exact match or a yes/no LLM judge.
5. Report accuracy for each position and the gap between best and worst. Fail CI if the gap is over about 10 points.

**What it catches:** whether your answer model depends on the reranker's order, which tells you whether to put the best chunks first, put them at both ends, or send fewer chunks. It also catches regressions after a model swap.

**Who runs it:** Devs run it in CI. Product sets the acceptable gap per use case. Architects use the results to set the ordering rule in the retrieval contract.