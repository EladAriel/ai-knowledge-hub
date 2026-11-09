# EVAL-011: Harness-Delta Attribution (HDA)

## Summary

An evaluation protocol that breaks down the improvement that automatic optimization of prompts, skills and tools produces into three parts.

## Content

**2. [Harness-Delta Attribution (HDA)](https://arxiv.org/abs/2610.22466)**, and next to it [Self-Evolving Agents Can Repair Failures but Struggle to Generalize](https://arxiv.org/abs/2610.22984)
- **What is it:** An evaluation protocol that breaks down the improvement that automatic optimization of prompts, skills and tools produces into three parts: overfitting to the search set, profit that comes from more compute, and what remains after both are removed.
- **Why new:** This wave has been back for two weeks: Harness Evolution on 10.10, Harness-RSI on 15.10, Harness² on 17.10 and Terminal-RSI on 18.10. This is the first time there is a tool to measure his claims.
- **Evidence:** Tested on 11 models and 3 frameworks. In 21 settings where a clear improvement was measured, on average 54% of it is overfitting and 14% comes s who learn from failures fix the tasks they failed on, but hardly improve on new tasks. There is no code.
- **Scores:** Effectiveness 4/5, hype 1/5.
- **Compatibility:** Mandatory for anyone who runs automatic optimization. effort *...on 14.10).
- **Evidence:** On Qwen3.5-9B, BFCL increased from 0.580 to 0.805, and DICE from 0.717 to 0.813. Most of the damage comes from distractions on the list. There is no code for either.
- **Scores:** Effectiveness 4/5, Hype 2/5.
- **Compatibility:** Any product with MCP. **low** effort.
- **Recommendation: Adopt** for the validation layer, **Pilot** for GatewayBench.

## Sources

- [Harness-Delta Attribution (HDA)](https://arxiv.org/abs/2610.22466)
- [Self-Evolving Agents Can Repair Failures but Struggle to Generalize](https://arxiv.org/abs/2610.22984)
