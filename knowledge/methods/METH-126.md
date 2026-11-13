# METH-126: ReTrace: distill an agent into a workflow without a planner

## Summary

Take an SOP and a few recorded agent runs. From the rationale the agent writes for each tool call, extract the condition behind every step. The result is a rules document and workflow code, so code—not an LLM—picks the next step.

## Details

What's new: the agent-to-workflow idea already exists; the trick here is using each call's rationale as the source of the branch condition, plus a repair loop that learns from failures. Evidence: on a production platform with 79 procedures, 93.8% completion vs 96.8% for the agent, at 24% lower cost. On τ²-Bench: 75.8% vs 80.6%, in 1.3 seconds instead of 170. The authors themselves note a limit: without the repair loop, ReTrace lags few-shot on SOP-Bench. No open source found. Scores: effectiveness 4/5, hype 1/5. Fit: high for any organisational product that runs the same processes over and over. Effort medium. Recommendation: Pilot. The theme of taking the LLM out of the hot loop continues after Strands Decider (Nov 10). arXiv 2611.14492.

## Sources

- [ReTrace (arXiv)](https://arxiv.org/abs/2611.14492)
