# METH-082: OpenAI Pando: Git backend built for agent-scale branches and pushes

## Summary

New Git backend for the volume of branches and pushes Codex generates: per-ref causal consistency instead of global consistency, and packfile reuse from a regional cache, fully compatible with the Git client.

## Details

Deliberately gives up a consistent snapshot of all refs to allow concurrent writes. Evidence: OpenAI production data: median push latency down ~80%, serving close to a petabyte per day; the simulation in the post is a demo model, not a benchmark. Not open source, but some improvements already landed in upstream Git. Fit: low–medium, for platforms running many coding agents in parallel on the same repo. Recommendation: Watch; echoes Anthropic Scion (Oct 16): source control for the agent era is becoming a category.

## Content

**5. [OpenAI Pando: Scaling Git at Agents](https://openai.com/index/scaling-git-at-openai/)**
- **What is it:** A new backend for Git, built for the amount of branches and pushes that Codex produces. It gives causal consistency to each ref separately instead of global consistency, and reuses packfiles from a regional cache.
- **Why new:** It intentionally foregoes a consistent snapshot of all refs to allow simultaneous writing, and remains fully compatible with the Git client.
- **Evidence:**
  - OpenAI production data: the median latency of push has decreased by about 80%, and it serves almost a petabyte per day.
  - The simulation in the post is presented as a demo model and not as a benchmark.
  - Not open source, but some improvements have already gone into Git upstream.
- **Scores:** Effectiveness 4/5 for those who reach this scale, hype 2/5.
- **Compatibility:** Low to medium, for platforms that run many code agents concurrently on the same repo. **high** effort.
- **Recommendation: Watch**. This repeats Anthropic Scion s becomes a category.

## Sources

- [OpenAI: Scaling Git at OpenAI](https://openai.com/index/scaling-git-at-openai/)