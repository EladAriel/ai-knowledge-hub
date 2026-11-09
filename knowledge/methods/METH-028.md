# METH-028: Good Judgment, Bad Advice: Decision-Model Controllers Raise Agent Cost

## Summary

A pre-planned experiment, with a placebo group, on Terminal-Bench 2.1.

## Content

**1. [Good Judgment, Bad Advice: Decision-Model Controllers Raise Agent Cost](https://arxiv.org/abs/2610.24649)** ([code](https://github.com/namanvats/decision-model-controllers))
- **What it is:** A pre-planned experiment, with a placebo group, on Terminal-Bench 2.1. The agent loop (Sonnet 5.5) remained constant, and only the controller that decides when to stop, when to verify and when to change access has changed. Five conditions were compared: no control, fixed rules, Haiku, Jev 1.13, and a randomized placebo control.
- **Why new:** This is the first end-to-end test of the "decision model as cheap as cattle", which came back with us this month on the 10th, 13th, 14th and 16th of the month. The result is negative.
- **Evidence:**
  - In 315 attempts, Jev will make the run more expensive by about 19% without any improvement in success (73% vs. 73%).
  - The placebo achieved the same success at a lower cost.
  - Jev ranks well (AUROC 0.78), but he is not calibrated: 87% of the agent's termination requests were correct, and he still asked for more verification.
  - **Limitation:** Only 21 tasks were tested, so the result on success is weak. The result on the cost is stable, with an increase in 15 of the 21 tasks.
- **Scores:** Effectiveness 4/5, hype 1/5.
- **Adjustment:** For anyone who adds a cheap controller or consultant above an agent loop. **low** effort.
- **Recommendation: Adopt** for the evaluation method: cost as the main measure, and comparison against fixed rules and against placebo. **Ignore** for an advisory controller that does not have calibrated thresholds.
- **Context:** This wraps up Jev's arc from this month. Already on 13.10 and 16.10 we saw that the local savings do not translate into results, and now there is a controlled experiment that shows it.

## Sources

- [Good Judgment, Bad Advice: Decision-Model Controllers Raise Agent Cost](https://arxiv.org/abs/2610.24649)
- [code](https://github.com/namanvats/decision-model-controllers)
