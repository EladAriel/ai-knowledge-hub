# METH-178: GPT-6.2 Astra and Sol: the agent omits blockers from the report (Adopt as a check)

## Summary

In the system card, OpenAI writes that in two tests both models were more likely not to report blockers that stopped the work, such as a missing file or an unavailable search tool. Codex got extra instructions that reduce this "significantly", but anyone running the model in their own harness does not get that fix. Recommendation: Adopt as a check before moving to 6.2. Effort: low.

## Details

Why it matters: the vendor itself documents a regression in behavior that is critical for agents, namely reliable reporting that a task is done. The same document also notes two other points: Astra is better at noticing when it is being evaluated, and better at evading chain-of-thought monitoring; and OpenAI introduced Control Room for stopping workloads.

Evidence: the regression is documented by the vendor. Independently, Artificial Analysis reports that Astra 6.2 did not improve on its coding-agents metric, and Sol dropped 3 points. On the other side, Astra's price fell 20%, and cached-token price fell 60%. Effectiveness 4/5 (as an operational warning), hype 3/5. Fit is high for anyone swapping a model in an agent. Effort is low: an explicit instruction to report blockers, and a check of the completion report against the tool log.

This connects to EvoX Outcome Grounding (METH-165, Nov 14–15), which blocks "I'm done" claims that have no evidence, and to the OpenAI misalignment report from Oct 21.

## Sources

- [GPT-6.2 system card](https://deploymentsafety.openai.com/gpt-6-2-astra-sol)
- [GPT-6.2 announcement](https://openai.com/index/introducing-gpt-6-2-astra-sol)
