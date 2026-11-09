# METH-084: Length Is Cheap, Competition Is Not: rival statements, not long context, cause context rot

## Summary

Neutral filler up to 32K tokens cost almost nothing; a single conflicting statement about the same fact multiplied the loss 9 to 110 times. For a Company Brain, two versions of the same policy in context are far worse than a long context.

## Details

Caveat: only small open models (0.5B-3B) were tested; code and data are public (yliusci/length-is-cheap). Adopt for: Architects dedupe before indexing and mark old versions as replaced so each fact has one 'current' flag; Product tracks 'conflicting sources' as its own failure type; Devs: when several retrieved chunks give a different value (rest of this part was cut off in the transcript). Term: rival statement = a same-format statement giving a different value for the same fact.

## Sources

- [Length Is Cheap, Competition Is Not (arXiv)](https://arxiv.org/abs/2611.04169)
- [code and data](https://github.com/yliusci/length-is-cheap)
