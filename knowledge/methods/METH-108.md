# METH-108: Meta²: Meta-Skill for when to act/hold/abstain + run-local harness edits

## Summary

Instead of training one shared harness offline, learn a textual Meta-Skill (when to act, hold, abstain) from A/B/C comparisons on training rollouts. At runtime an evolver edits the harness only inside the current run from checkpoints, without drifting verifier feedback.

## Details

What's new: hybrid separating 'how to edit' knowledge (global) from harness edits (local to the run)—answers Continual Harness / Meta-Harness / AHE. Evidence: Terminal-Bench 2.1 with GPT-5.6-Terra 81.0% (+14.67 vs NexAU seed); DeepSWE 1.1 44.44% (+9.77); also leads on DeepSeek-V4-Flash; high one-time offline cost; resetting harness between tasks matters (ablation). Scores: effectiveness 4/5, hype 3/5. Fit: high for long-horizon and coding agents. Effort: high. Recommendation: Pilot. Continues harness-RSI wave.

## Sources

- [Meta² (arXiv)](https://arxiv.org/abs/2611.05139)
