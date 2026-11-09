# METH-071: Routed Continual Learning (FAIR, Meta)

## Summary

Before each run an LLM router picks the memory 'cluster' and memory type (full-history ICL, ReasoningBank or a statistical model); memory is injected into context without changing the agent.

## Details

Treats continual learning as a routing problem instead of one global memory: what to keep and whom to share with is decided per task. Tested on 398 mixed tasks from CL-Bench and τ³-Bench, 4 models, 5 runs: beats Global ICL by 15-30% of max reward at 65-72% lower API cost; Global ICL barely helps when tasks are mixed. Limits: no parallel updates or cross-model memory tested; router sometimes over-splits (23-86 clusters). Fit: high for enterprise assistants serving many task types.

## Content

**1. [Routed Continual Learning (FAIR, Meta)](https://arxiv.org/abs/2610.38796)**
- **What it is:** Before each run, LLM Router decides to which memory "cluster" it belongs and what kind of memory it will hold. The options are Complete History (ICL), ReasoningBank or Statistical Model. The memory is injected into the context of the agent without changing the agent itself.
- **Why this is new:** Instead of "one global memory for all" it treats continuous learning as a routing problem. Both what is held and with whom is shared is determined for each task.
- **Evidence:** Tested on 398 tasks mixed from CL-Bench and τ³-Bench, with 4 models and 5 runs. It is superior to Global ICL by 15–30% of maximum reward, 65–72% lower API cost. Global ICL, which won the original CL-Bench, was also found to be of little help when the tasks were mixed. Limitations the authors note: parallel updates or cross-model memory were not tested, and the router sometimes oversplits (23–86 clusters).
- **Scores:** Effectiveness 4/5, hype 1/5
- **Suitability:** High for organizational assistants who serve many types of tasks. Medium effort.
- **Recommendation: Pilot.** This continues the "Harmful Global Memory" wave from October 21st, 23rd and 26th, and this time with a concrete solution.

## Sources

- [Routed Continual Learning](https://arxiv.org/abs/2610.38796)