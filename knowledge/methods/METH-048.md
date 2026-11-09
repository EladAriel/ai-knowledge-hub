# METH-048: Agent S4: Evolving Agent Interfaces (Simular)

## Summary

A meta-agent reads running tracks of a computer-use agent on synthetic tasks, without success labels, and builds a library of new interfaces and tools for it.

## Content

### 1. [Agent S4: Evolving Agent Interfaces (Simular)](https://arxiv.org/abs/2610.28601)
[repo](https://github.com/simular-ai/Agent-S)
- **What it is:** A meta-agent reads computer-use agent run paths on synthetic tasks, without success labels, and builds a library of new interfaces and tools for it. For example, writing code instead of typing a sheet cell by cell. Population-based evolution chooses which libraries to continue evolving, according to validation tasks that the metaagent has not seen.
- **Why new:** Until now, "harness development" has improved prompts and flow. Here what develops is the operation interface itself, without changing weights. The subject of a harness that improves itself comes up for the fifth time in two weeks.
- **Evidence:**
  - According to the article, Qwen3.8-27B reached 21.3% in OSWorld V2. This is 3.8 times more than the same model with fixed interfaces, and more than GPT-5.5 (13.0%) and Opus 4.8 (20.6%).
  - The cost is about $1.10 per mission.
  - In ScienceBoard the score increased from 41.4% to 58.6%.
  - The code is open, but all the numbers are from Simular, and there is no independent recovery yet.
- **Scores:** Effectiveness 4/5, Hype 4/5.
- **Fit:** High for any product with an agent that runs a UI or tools. **medium to high** effort. The immediate lesson: it's worth investing in the tool interfaces before replacing a model.
- **Recommendation: Pilot**

## Sources

- [Agent S4: Evolving Agent Interfaces (Simular)](https://arxiv.org/abs/2610.28601)
- [repo](https://github.com/simular-ai/Agent-S)
