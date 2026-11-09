# METH-004: STEPGATE: Escalation from a small model to the cloud at the step level

## Summary

A small, local model runs the agent and gives each step an uncertainty score.

## Content

**3. [STEPGATE: Escalating from a small model to the cloud at the step level](https://arxiv.org/abs/2610.07816)**
- **What it is:** A small, local model runs the agent and gives each step an uncertainty score. Only the difficult steps are transferred to a more powerful model.
- **Why new:** Normal routers choose a model once for each query, and here the decision is made anew at each step.
- **Evidence:** In the test based on BFCL, he reached 82.7% success, with 30.8% of the steps being escalated. A local model alone reached 67.3%, and the escalation is...n- **Scores:** Effectiveness 3/5, Hype 1/5.
- **Adjustment and Effort:** Suitable for any assistant who has a personal memory. **low** effort.
- **Recommendation: Pilot**

## Sources

- [STEPGATE: Escalation from a small model to the cloud at the step level](https://arxiv.org/abs/2610.07816)
