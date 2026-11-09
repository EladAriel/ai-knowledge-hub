# METH-078: Agentic World Modeling (AWM, Microsoft): test-time scaling

## Summary

Agentic World Modeling predicts the outcome of each action with read-only queries against the real environment plus computation, instead of running parallel trajectories in an environment that cannot be cloned or reset. Evidence gathering happens over several steps without changing shared state. Reported averages are about 40% above one-shot simulation and 12% above a trained world model on τ-bench, AppWorld, and OfficeBench.

## Details

Unlike world models that compress environment state into a single prompt, this approach treats prediction as multi-step evidence collection. No public code or independent reproduction was noted in the source write-up.

## Sources

- [Agentic World Modeling](https://arxiv.org/abs/2610.40927)
