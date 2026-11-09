# METH-005: MASS: Multi-Agent Self-Supervision

## Summary

What it is: Sakana and Berkeley method. The same model is used as a solver, as someone who improves the workflow of the agent team and also as an evaluator. After two rounds he is coached on the runs of the team that did the best. - Why it's new: It's not another harness improvement. What the team learned fed back into the model's weights.

## Content

**1. [MASS: Multi-Agent Self-Supervision](https://sakana.ai/mass/)** ([Article](https://arxiv.org/abs/2610.12176), [Code](https://github.com/SakanaAI/mass))
- **What it is:** Method of Sakana and Berkeley. The same model is used as a solver, as someone who improves the workflow of the agent team and also as an evaluator. After two rounds he is coached on the runs of the team that did the best.
- **Why is this new:** This is not another harness improvement. What the team learned fed back into the model's weights.
- **Evidence:** Tested with Qwen3.6-27B on four research missions. The score in relation to the amount of output tokens increased 1.2 to 1.6 times, and the win rate increased from 53.9% to 69.9%. The researchers state that there was no improvement in SWE-bench and Terminal-Bench. They also warn that when a model improves itself, its "blind spots" are common to all roles.
- **Scores:** Effectiveness 4/5, Hype 3/5.
- **Compatibility and effort:** High for research and code agents. **high** effort.
- **Recommendation: Pilot**

## Sources

- [MASS: Multi-Agent Self-Supervision](https://sakana.ai/mass/)
- [article](https://arxiv.org/abs/2610.12176)
- [code](https://github.com/SakanaAI/mass)
