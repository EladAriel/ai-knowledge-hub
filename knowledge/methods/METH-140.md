# METH-140: WorkflowArena: a benchmark for workflow orchestration

## Summary

145 long tasks in 8 domains, including software engineering, finance, law, formal mathematics and 3D. The agent itself decides whether and how to delegate work to sub-agents, and every delegation is recorded. Code: github.com/Einsia/WorkflowArena. arXiv 2611.12856.

## Details

What's new: the benchmark measures the quality of work organization as a separate ability, not only the end product. A notable finding: a workflow that Opus 5.5 wrote improved weaker models by 6.41 points on average. Evidence: there is code, data and a results file. Best result: Opus 5.5 at maximum thinking fully solved 36.95% of the tasks. The authors themselves note that each task was run once with no measure of variance, so close rankings are not reliable. The repo is new, with 8 stars. Scores: effectiveness 3/5, hype 2/5. Fit: anyone building a multi-agent system and considering letting the model write the workflow at run time. The pattern of a strong model that writes and a cheap model that executes ties directly to ReTrace (Nov 11). Effort: medium. Recommendation: Pilot as an eval, on the subset relevant to your domain.

## Sources

- [WorkflowArena (arXiv)](https://arxiv.org/abs/2611.12856)
- [WorkflowArena code](https://github.com/Einsia/WorkflowArena)
