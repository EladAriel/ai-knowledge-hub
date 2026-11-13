# METH-104: The Intrusion Pathway: irrelevant context still hurts

## Summary

Padding the prompt with unrelated text lowers accuracy even when the padding has no competing answer and nothing in common with the question. Comes from a small set of attention heads; turning off ~10 (~1% of the model) recovered ~57% of the loss across math, multi-hop and medical sets.

## Details

How it fits: chunk order matters (prior brief); conflicting statements hurt; now even plain noise with no conflict hurts. Effort: high to change the model itself; cheap fix is to filter hard before generating and not pad with 'background' text. Adopt for: Architects / Product / Devs—filter non-evidence context before generation. Code: dk4248/the-intrusion-pathway.

## Sources

- [Intrusion Pathway (arXiv)](https://arxiv.org/abs/2611.07778)
- [code](https://github.com/dk4248/the-intrusion-pathway)
