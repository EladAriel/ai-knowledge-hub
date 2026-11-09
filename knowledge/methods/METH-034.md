# METH-034: The counter wave to memory agents: More Memory, Worse Agents, MemDev-Bench, REM

## Summary

Three papers published on the same day against cumulative agent memory.

## Details

More Memory, Worse Agents: rules and summaries that the agent keeps from his experience make him repeat the same mistakes. ... Company brain (Oct 21): log which memory each answer used, so failures can be traced back to it.

## Content

**2. Counter wave for memory agents: [More Memory, Worse Agents](https://arxiv.org/abs/2610.27406), [MemDev-Bench](https://arxiv.org/abs/2610.27524), [REM](https://arxiv.org/abs/2610.27377)**
- **What is it:** Three articles published on the same day:
  - **More Memory, Worse Agents:** Rules and summaries that the agent keeps from his experience make him repeat the same mistakes. The solution that the article offers, Anti-Persistence, only saves routes and results, and generates a temporary prompt for each new task.
  - **MemDev-Bench:** Memory also breaks tasks that the agent would have solved without it, because it does not check if ...3 points in HN). Includes deterministic sampling, and is mainly relevant for those who host models themselves.
- [SlopCodeBench, October update](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/benchmarking-new-models-on-slop-code-bench.md): On Opus 5.5, xhigh effort came out worse than medium, at 2 to 4 times higher cost. It's one run per setup, so it's still inconclusive.
- [Backdoor in abliterated models](https://projectdiscovery.io/research/how-abliterated-models-can-get-you-pwned): A poisoned model steals .env files via Codex CLI when a trigger word appears.
- [Fake Stats Cited in LLMs](https://peec.ai/blog/publish-stats-get-cited-the-tactic-that-put-my-data-all-over-the-web): Site with 50,000 made up data cited on ChatGPT. Relevant to RAG from Hobb.
- [RiseHarness](https://arxiv.org/abs/2610.27435): Harness improvement using tasks that the same setting both succeeds and fails at.
- [KEEP-Bench](https://arxiv.org/abs/2610.26827): Checks if context compression preserves the evidence. The best model kept them all only 66.8% of the time.- [RITE](https://arxiv.org/abs/2610.27777): Silent tool errors cut agent success by about half.
- [PROVISO](https://arxiv.org/abs/2610.27115): Selects actions according to the source of information, before execution.
- [EGI-BENCH](https://arxiv.org/abs/2610.27234): Eight enterprise benchmarks under one CLI.
- [PORA](https://arxiv.org/abs/2610.27119): learning when long reasoning is worth the budget.
- **System One / Decision-1:** keeps repeating ([2610.27099](https://arxiv.org/abs/2610.27099), [2610.26444](https://arxiv.org/abs/2610.26444), [2610.28435](https://arxiv.org/abs/2610.28435)), and it seems that it is already a genre.

## Sources

- [More Memory, Worse Agents](https://arxiv.org/abs/2610.27406)
- [MemDev-Bench](https://arxiv.org/abs/2610.27524)
- [REM](https://arxiv.org/abs/2610.27377)
- [SlopCodeBench, October update](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/benchmarking-new-models-on-slop-code-bench.md)
- [Backdoor in abliterated models](https://projectdiscovery.io/research/how-abliterated-models-can-get-you-pwned)
- [Fake statistics quoted in LLMs](https://peec.ai/blog/publish-stats-get-cited-the-tactic-that-put-my-data-all-over-the-web)
- [RiseHarness](https://arxiv.org/abs/2610.27435)
- [KEEP-Bench](https://arxiv.org/abs/2610.26827)
- [RITE](https://arxiv.org/abs/2610.27777)
- [PROVISO](https://arxiv.org/abs/2610.27115)
- [EGI-BENCH](https://arxiv.org/abs/2610.27234)
- [PORA](https://arxiv.org/abs/2610.27119)
- [2610.27099](https://arxiv.org/abs/2610.27099)
- [2610.26444](https://arxiv.org/abs/2610.26444)
- [2610.28435](https://arxiv.org/abs/2610.28435)