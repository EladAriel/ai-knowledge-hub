# METH-078: Agentic World Modeling (AWM, Microsoft): test-time scaling in a shared environment

## Summary

An agent simulator predicts the outcome of each action using read-only queries against the real environment and calculation, instead of running parallel paths in an environment that cannot be duplicated or reset.

## Content

**2. [Agentic World Modeling (AWM)](https://arxiv.org/abs/2610.40927)** (Microsoft)
- **What is it:** test-time scaling (investing more computation during runtime) for agents who work in a common environment that cannot be duplicated or reset, such as an organizational workspace. An agent simulator predicts what the outcome of each action will be. It does this with the help of read-only queries against the real environment and with the help of calculation.
- **Why new:** Existing world models compress the state of the environment into one prompt. Here the prediction is gathering evidence in several steps, without changing anything in the joint situation.
- **Evidence:**
  - On average 40% above a one-time simulation and 12% above a trained world model, on τ-bench, AppWorld and OfficeBench.
  - I did not find a code, and there is no restoration of commissions, and all mutations were rejected.
  - The promises are only valid for the defined profile.
  - No external adoption.
- **Scores:** Effectiveness 3/5, Hype 1/5.
- **Adjustment:** medium-high. Re-authentication at the moment of execution is cheap, and the full protocol is heavy. **high** effort for full realization.
- **Recommendation: Watch.** The re-verification at the moment of execution should be adopted now. The subject repeats: control of agents has been repeatedly raised since 10.25.

## Sources

- [Agentic World Modeling](https://arxiv.org/abs/2610.40927)
