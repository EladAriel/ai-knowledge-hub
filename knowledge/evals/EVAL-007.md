# EVAL-007: Eval: citation correctness (ALCE recall/precision)

## Summary

For every claim, check the cited chunks support it: citation recall and citation precision.

## Details

1) Structured output [{claim, chunk_ids}]. 2) Log cited chunk text. 3) Code checks first: cited IDs were retrieved, user may see them, flag uncited claims. ….

## Sources

- [ALCE (Gao et al.)](https://arxiv.org/abs/2305.14627)
- [Wallat et al.](https://arxiv.org/abs/2412.18004)
