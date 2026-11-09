# METH-006: RATED: Retrieving tools according to reliability

## Summary

Semantic retrieval of tools, plus a bandit algorithm that reranks them according to successes and failures at runtime.

## Content

**2. [RATED: tool retrieval by reliability](https://arxiv.org/abs/2610.13889)** (CIKM 2026, [code](https://github.com/Elliotes/EcoAgent))
- **What it is:** Semantic retrieval of tools, plus a bandit algorithm that reranks them according to successes and failures at runtime. There is no need to retrain the planner.
- **Why this is new:** Standard ToolRAG is static. Here there is an explicit model for tools that break or fall.
- **Evidence:** MRR (Index of Ranking Quality) is 52% higher than ToolLLM. When 30% of the tools are unavailable, the choice of broken tools drops from 86% to 2.9%. The overhead is less than a millisecond. The test ran on 5,172 real tools from LangChain, CrewAI, LlamaIndex and n8n.
- **Scores:** Effectiveness 5/5, hype 2/5.
- **Compatibility and effort:** Very high for any enterprise product with many tools. **medium** effort.
- **Recommendation: Pilot**. This is today's powerful item.

## Sources

- [RATED: Retrieving tools according to reliability](https://arxiv.org/abs/2610.13889)
- [code](https://github.com/Elliotes/EcoAgent)
