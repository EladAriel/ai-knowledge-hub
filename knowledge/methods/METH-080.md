# METH-080: Fidelity Synopses: vector-index setting chosen per query

## Summary

Instead of one vector-index setting for every query (paying for the hardest case every time), a small precomputed lookup table predicts which cheaper setting still returns enough of the true top-k for each query.

## Details

Fidelity = share of the exact top-k that an approximate index actually returns. Fidelity synopsis = precomputed table predicting fidelity per region of the embedding space for each index setting. Results: at the same quality target, median cost 0.72x the fixed setup; the lookup takes 21–32 microseconds. Research only so far.

## Sources

- [Fidelity Synopses (arXiv)](https://arxiv.org/abs/2610.41407)
