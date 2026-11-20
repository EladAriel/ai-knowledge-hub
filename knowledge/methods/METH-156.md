# METH-156: Declining to answer is fragile both ways: prompt thresholds don't move, and fake warnings trigger refusals

## Summary

Telling 12 small open models they may say "I abstain" raised how often they declined from 20% to 91%, but raising the stated threshold from 0.5 to 0.9 moved abstention by only −0.8 points. Fake "compliance hold" notes in low-trust content made agents refuse legitimate work, and a caution-first system prompt made this worse. Effort: medium.

## Details

Threshold paper (arXiv 2611.14661): up to 40% of a checkpoint's items got decisions that no threshold-following policy could make. A threshold applied outside the model on recalibrated P(True) made coverage behave correctly by construction. It also has limits: calibrated on TriviaQA and applied to PopQA, it fell below the abstain-format prompt at t=0.75. Attack paper (arXiv 2611.14864): a caution-first system prompt amplified the attack — Gemini-3-flash went from 9.8% to 86.3% induced over-abstention while clean-task completion stayed at 96%. A Verify-Before-Abstain prompt (check the warning against authoritative records first) restored completion to 73–100% on a 15-pair subset. It did not consistently protect confidential content, and it relies on oracle provenance tags. Adopt for: Architects keep the answer/abstain threshold and the source-authority tiers in code and config, not in the prompt, and require corroboration from the system of record; Product set the threshold per risk tier (HR/finance stricter than how-to) and report coverage alongside accuracy, not abstention rate alone; Devs, in CI, assert that coverage is non-increasing as the threshold rises, and plant 10 fake-warning docs to measure induced refusals (see EVAL-041).

## Sources

- [Abstention threshold paper](https://arxiv.org/abs/2611.14661)
- [Fake-warning over-abstention](https://arxiv.org/abs/2611.14864)
