# METH-080: Fidelity Synopses: vector-index setting chosen per query

## Summary

Instead of one vector-index setting for every query (paying for the hardest case every time), a small precomputed lookup table predicts which cheaper setting still returns enough of the true top-k for each query.

## Details

Fidelity = share of the exact top-k that an approximate index actually returns. Fidelity synopsis = precomputed table predicting fidelity per region of the embedding space for each index setting. Results: at the same quality target, median cost 0.72x the fixed setup; the lookup takes 21–32 microseconds. Research only so far.

## Content

**2. [Fidelity Synopses: index settings chosen per query](https://arxiv.org/abs/2610.41407)**
- **The problem:** most teams use one vector-index setting for every query, so every query pays for the hardest case.
- **The fix:** a small lookup table predicts which cheaper setting still finds enough of the true top results for each query.
- **Results:** at the same quality target, median cost dropped to 0.72 times the fixed setup, and the lookup takes 21–32 microseconds. It's research only so far.
- Adopt for:
  - *Architects:* write the recall ta... **Pattern:** third time after Tether and StateGraph. Derived facts need to track what they were computed from.
- Adopt for:
  - *Architects:* keep raw records as the source of truth, and make derived values something you can recompute.
  - *Product:* tell users why a value changed, like "updated because X changed," to build trust.
  - *Devs:* compute derived fields with code over typed records, not with free-text LLM rewrites.

## Sources

- [Fidelity Synopses (arXiv)](https://arxiv.org/abs/2610.41407)