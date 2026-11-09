# METH-065: The Coordination Tax and the Heterogeneity Dividend

## Summary

A closed model that weighs the cost of a multi-agent pipeline (decomposing the task and each handoff) against the savings when roles are transferred to a cheap model.

## Content

**1. [The Coordination Tax and the Heterogeneity Dividend: the coordination tax versus the heterogeneity dividend] (https://arxiv.org/abs/2610.37700)**
- **What is it:** A closed model that weighs the cost of a multi-agent pipeline, i.e. the breakdown of the task and any handoff between agents, against the savings obtained when roles are transferred to a cheap model. Measured on 135 code tasks, in 2,430 runs of six architectures.
- **Why new:** The "one agent or many" debate has been around for a long time. The innovation is a break-even formula that can be measured.
- **Evidence:**
  - The planner-coder-reviewer pipeline costs 3.22 times, is 3.24 times slower, and does not solve more tasks.
  - When transferring roles to a cheap model, the cost drops to 0.39 of the original, but the accuracy drops by 6.7 points.
  - Choosing one suitable model for each task (oracle) solves 94.3% of the tasks, at half the cost.
  - Tested only on code tasks and with two models. There is no code.
- **Scores:** Effectiveness 4/5, hype 1/5.
- **Suitability:** High for anyone who builds multi-agency pipelines. **low** effort.
- **Recommendation: Adopt** As a basis for comparison: before breaking down a task into several agents, compare to one strong call and routing of a model by task. This is the third time that the subject has come up, after 21.10 and 27.10, and each time the conclusion is the same.

## Sources

- [The Coordination Tax and the Heterogeneity Dividend: The coordination tax versus the heterogeneity dividend](https://arxiv.org/abs/2610.37700)
