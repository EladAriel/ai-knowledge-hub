# METH-179: FrontierHarness Eval v1.1: the best harness depends on the model (Adopt as a method)

## Summary

22 harnesses, 5 open models, 62 terminal tasks and 4 attempts per pair, about 27,000 runs in total, together with Baseten. On the cost ranking, the median harness moved 11 places out of 22 from one model to another, and Codex CLI fell from place 1 to 16. Recommendation: Adopt as a method — when you change the model, re-check the harness too. Effort: medium.

## Details

What is new: until now harnesses were compared on a single model. Here the pair of harness and model is measured as a unit.

Evidence: the method is documented, and 216 runs flagged as cheating were scored zero. Caveats: RUNTA sells runtime; only open models were tested, at default settings, and only terminal tasks. Effectiveness 4/5, hype 2/5. Fit is high for any agent product that chooses or swaps a model. Effort is medium because you need an internal eval for each pair.

The harness theme has come up almost every day: Nov 5, 6, 8 and 9 (g-harness-evals, EVAL-032), and EvoX on Nov 14–15 (METH-165).

## Sources

- [FrontierHarness Eval v1.1](https://runta.com/blog/introducing-frontierharness-eval-v1-1/)
