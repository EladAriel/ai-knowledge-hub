# METH-082: OpenAI Pando: Git backend built for agent-scale branches and pushes

## Summary

New Git backend for the volume of branches and pushes Codex generates: per-ref causal consistency instead of global consistency, and packfile reuse from a regional cache, fully compatible with the Git client.

## Details

Deliberately gives up a consistent snapshot of all refs to allow concurrent writes. Evidence: OpenAI production data: median push latency down ~80%, serving close to a petabyte per day; the simulation in the post is a demo model, not a benchmark. Not open source, but some improvements already landed in upstream Git. Fit: low–medium, for platforms running many coding agents in parallel on the same repo. Recommendation: Watch; echoes Anthropic Scion (Oct 16): source control for the agent era is becoming a category.

## Sources

- [OpenAI: Scaling Git at OpenAI](https://openai.com/index/scaling-git-at-openai/)
