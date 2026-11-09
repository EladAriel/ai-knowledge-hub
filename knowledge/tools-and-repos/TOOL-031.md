# TOOL-031: DLite: Speculative decoding for agent workloads

## Summary

In the work of the agents, the input is long and the output is short, and in such a situation normal draft models are enough to produce only 1 to 2 tokens that are received.

## Content

### 5. [DLite: Speculative Decoding for Agent Workloads](https://arxiv.org/abs/2610.23787) ([Code](https://github.com/SJTU-DAI-Sys/DLite))
- **What is it:** In the work of the agents, the input is long and the output is short, and in such a situation normal draft models are sufficient to produce only 1 to 2 tokens that are received. DLite forgoes the KV cache on the draft model side, and reuses the hidden states of the target model.
- **Evidence:**
  - The code and weights are open.
  - In SWE-bench, with the connection of 40K to 64K tokens, the acceleration is 2.7 times, compared to 1.6 times in DSpark.
  - Only tested on Qwen3-4B and Qwen3-8B.
- **Scores:** Effectiveness 4/5, Hype 2/5.
- **Compatibility:** Only for those who host models themselves. **medium to high** effort.
- **Recommendation: Pilot** for those who host themselves, **Watch** for everyone else. On 19.10 it appeared only in the list of terms, and this week the discussion around it started with X.

## Sources

- [DLite: Speculative decoding for agent workloads](https://arxiv.org/abs/2610.23787)
- [code](https://github.com/SJTU-DAI-Sys/DLite)
