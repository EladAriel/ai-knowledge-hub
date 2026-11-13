# EVAL-032: g-harness-evals (Garry Tan): same model across 7 harnesses

## Summary

Holds the model (Opus 5.5 or GPT-6.1 Sol) and 20 tasks fixed and swaps only the harness (Claude Code, Codex, Hermes, OpenClaw, QM), measuring success rate, cost per solved task and time. Success rates 71-79% are statistically indistinguishable, but cost differs ~2x ($0.19-$0.44 per task on Opus).

## Details

Not a new idea; an open comparison with preregistration and confidence intervals. Evidence: code and data open; the author cautions 14 of 20 tasks are too easy and a Terminal-Bench run is coming; confidence intervals are wide. Scores: effectiveness 3/5, hype 3/5 (big name, ~78k views). Fit: choose a harness by cost and speed, and build your own regression suite. Effort: low. Recommendation: Adopt the methodology, not the ranking. Continues the harness theme after Nov 5, 6 and 8.

## Content

**2. [Garry Tan's g-harness-evals: same model, 7 harnesses](https://github.com/garrytan/g-harness-evals)**
- **What it is:** the model (Opus 5.5 or GPT-6.1 Sol) and the 20 tasks stay fixed, and only the harness is swapped: Claude Code, Codex, Hermes, OpenClaw and QM. It measures success rate, cost per solved task, and time.
- **Why it's new:** it is not a new idea, but an open comparison with preregistration and confidence intervals. The success rates, 71% to 79%, are statistically indistinguishable from each other. Cost, by contrast, differs by a factor of 2: $0.19 to $0.44 per task on Opus.
- **Evidence:**
  - The code and data are open.
  - The author cautions that 14 of the 20 tasks are too easy, and a Terminal-Bench run is on the way.
  - The confidence intervals are wide.
- **Scores:** effectiveness 3/5, hype 3/5 (big name, ~78k views).
- **Fit:** choose a harness by cost and speed, and build your own regression suite. Effort: low.
- **Recommendation:** Adopt the methodology, not the ranking.

## Sources

- [g-harness-evals](https://github.com/garrytan/g-harness-evals)
