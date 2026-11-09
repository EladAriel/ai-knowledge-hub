# METH-007: T²Mem: Memory built at query time

## Summary

What it is: In advance, only light metadata is saved on each call.

## Content

**3. [T²Mem: memory built at query time](https://arxiv.org/abs/2610.13348)** ([code](https://github.com/OpenBMB/T2Mem))
- **What is it:** In advance, only light metadata is saved on each call. When a query arrives, the LLM builds a memory that is adapted to it, by searching the metadata and...* A subagent can stop in the middle of a run and ask the orchestrator to change its goal, tools, context or budget. OPOD turns this feedback into training data for the orchestrator.
- **Why is this new:** The adjustment happens during the execution, and not only at the end of the run.
- **Evidence:** On GAIA and SWE-Bench there is an improvement of about 9% compared to the strongest baseline. A small orchestrator (Qwen3.5-9B) with OPOD improved by about 10%. In the meantime there are only experiments on benchmarks.
- **Scores:** Effectiveness 4/5, Hype 3/5.
- **Adaptation and Effort:** High for dynamic multi-agent systems. **high** effort.
- **Recommendation: Pilot**

**Repeats again:** The theme of memory continues for the third day in a row (T²Mem, SEEDS). Also the idea of ​​escalation within the run, from a cheap model to a powerful model, returns after STEPGATE (ARIA).

## Sources

- [T²Mem: Memory built at query time](https://arxiv.org/abs/2610.13348)
- [code](https://github.com/OpenBMB/T2Mem)
