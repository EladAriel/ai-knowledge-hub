# METH-146: Wayfinder: learn where to search from what agents cite

## Summary

Agents keep re-searching Slack, tickets, email and wikis to answer things like "what was decided last meeting." Wayfinder learns which source to search first from the documents the agent actually cited (arXiv 2611.16053, NeurIPS 2026). Effort: medium.

## Details

It helps only when sources overlap in content. When they're clearly different, picking a tool from a good description is enough. The tests use public datasets, not real company data. Rebrand watch: this is "resource selection" from classic federated search, now learned from citations. Adopt for: Architects log which source each cited document came from — that log is what you'd train a router on later; Product track how many sources get searched per answer, as a cost metric; Devs start with good tool descriptions, and only add a learned router if your sources overlap.

## Sources

- [Wayfinder](https://arxiv.org/abs/2611.16053)
