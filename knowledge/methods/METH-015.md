# METH-015: Decision models that share control with the LLM: JevAgentHarness and Jev-LiteMAS

## Summary

Most calls to LLM in harness end with a choice of several options, for example which tool to run.

## Content

**2. Decision models that share control with the LLM: [JevAgentHarness](https://arxiv.org/abs/2610.21412) ([code](https://github.com/JevAgentHarness/JevAgentHarness)) and [Jev-LiteMAS](https://arxiv.org/abs/2610.21411)**
- **What is it:** Most of the calls to LLM in harness end with a choice from several options, for example which tool to run. A cheap decision model meets these choices, and the large LLM comes in only when the confidence of the decision model is lower than a threshold that is calibrated for each type of decision.
- **Why new:** This is mainly an incarnation of model cascading (FrugalGPT style). The new thing is that the transition between the models happens at a single decision level, and that there is an open model of size 4B that was trained on situations that the agent reaches after his own mistakes.
- **Evidence:**
  - The important finding is actually negative. The decision model that was the most accurate on individual questions solved only 69.5% of the tasks, and when we let it choose tools without a calibrated threshold, success dropped by 19 points.
  - With a calibrated threshold, the authors report 81% to 89% cost savings and up to 2.5x faster running, with less than a 3-point drop in success.
  - The models and data are not yet parallel. Scion itself requires a **high** effort.
- **Recommendation: Watch.** The superfans pattern is worth trying in Pilot, because it fits almost every team and with little effort.

## Sources

- [JevAgentHarness](https://arxiv.org/abs/2610.21412)
- [code](https://github.com/JevAgentHarness/JevAgentHarness)
- [Jev-LiteMAS](https://arxiv.org/abs/2610.21411)
