# PIPE-005: Pipeline: agent and answer layer

## Summary

question + identity -> plan sub-queries -> hybrid search over a navigation layer -> fetch sources -> draft -> validate ….

## Details

Enforce the evidence contract in code (reject citations that aren't exact substrings). Let the agent search again after drafting. Answer only with the asker's access; run writes under the user's own connection. ….

## Sources

- [Airbnb](https://arxiv.org/abs/2610.14428)
- [Memory Echo](https://arxiv.org/abs/2610.17763)
- [company-brain permissions](https://github.com/supermemoryai/company-brain/blob/main/docs/guide/permissions.md)
