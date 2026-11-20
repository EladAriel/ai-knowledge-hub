# EVAL-032: g-harness-evals (Garry Tan): same model across 7 harnesses

## Summary

Holds the model (Opus 5.5 or GPT-6.1 Sol) and 20 tasks fixed and swaps only the harness (Claude Code, Codex, Hermes, OpenClaw, QM), measuring success rate, cost per solved task and time. Success rates 71-79% are statistically indistinguishable, but cost differs ~2x ($0.19-$0.44 per task on Opus).

## Details

Not a new idea; an open comparison with preregistration and confidence intervals. Evidence: code and data open; the author cautions 14 of 20 tasks are too easy and a Terminal-Bench run is coming; confidence intervals are wide. Scores: effectiveness 3/5, hype 3/5 (big name, ~78k views). Fit: choose a harness by cost and speed, and build your own regression suite. Effort: low. Recommendation: Adopt the methodology, not the ranking. Continues the harness theme after Nov 5, 6 and 8.

Nov 18 update: FrontierHarness Eval v1.1 continues this line (see METH-179). It ran 22 harnesses with 5 open models on 62 terminal tasks, 4 attempts per pair (about 27,000 runs, together with Baseten). On the cost ranking, the median harness moved 11 places out of 22 from one model to another, and Codex CLI fell from place 1 to 16. The lesson: the best harness depends on the model, so when you change the model, re-check the harness too.

## Content

### g-harness-evals by Garry Tan: same model, 7 harnesses

- **What it is:** the model (Opus 5.5 or GPT-6.1 Sol) and the 20 tasks are fixed, and only the harness is swapped: Claude Code, Codex, Hermes, OpenClaw and QM. Success rate, cost per solved task and time are measured.
- **Why it's new:** it isn't a new idea, but an open comparison with preregistration and confidence intervals. The success rates, 71% to 79%, can't be told apart from one another. The cost, on the other hand, differs by 2x: $0.19 to $0.44 per task on Opus.
- **Evidence:**
  - The code and data are open.
  - The author cautions that 14 of the 20 tasks are too easy, and a Terminal-Bench run is still on the way.
  - The confidence intervals are wide.
- **Scores:** effectiveness 3/5, hype 3/5 (the source note was cut off at this point).

## Sources

- [g-harness-evals](https://github.com/garrytan/g-harness-evals)
- [FrontierHarness Eval v1.1](https://runta.com/blog/introducing-frontierharness-eval-v1-1/)
