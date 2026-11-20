# METH-166: guardscope: what runtime controls actually check

## Summary

A framework that measures which share of the agent's actions actually go through the control gate, including bypasses through the shell, the network and files, not only tool calls. Code: VulcanLab/guardscope (arXiv 2611.15223). A Nov 15 review lowered effectiveness to 3/5 and refined the recommendation.

## Details

It works in two stages: a static analysis of 15 action paths, and an empirical run that classifies each action as checked, bypassed or blocked, against a kernel-level ground truth. Existing tests evaluate controls only on tool calls; this measures coverage of every path. The code is open. Nov 15 update: only some of the 15 paths were covered empirically (4 of 15), "checked" does not mean the policy is correct, and there was no test against an attacker; the repo has no stars. Effectiveness was lowered to 3/5. The refined recommendation: adopt the method — map all of the agent's action paths, not only tool calls — and Watch the tool itself.

## Sources

- [guardscope](https://arxiv.org/abs/2611.15223)
- [VulcanLab/guardscope](https://github.com/VulcanLab/guardscope)
