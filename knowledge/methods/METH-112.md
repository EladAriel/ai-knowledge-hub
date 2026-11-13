# METH-112: ENGRAM: check before you drop a memory

## Summary

An agent's past experience is used to train the model. A stored memory is removed from search only after a test shows the trained model, without search, does better than the original model with search.

## Details

Results on HotpotQA: with that check, accuracy stayed at 70.9 vs 71.1 for keeping everything, while 55% fewer memories stayed searchable; removing memories right after training dropped accuracy to 66.8. Adopt for: run the golden set with and without the memories you plan to remove; block the cleanup if quality drops. Continues the 'prove nothing is lost before you compress or forget' theme.

## Sources

- [ENGRAM (arXiv 2611.09472)](https://arxiv.org/abs/2611.09472)
