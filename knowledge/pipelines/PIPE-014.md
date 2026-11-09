# PIPE-014: Pipeline: gated agent/answer layer with code checks

## Summary

question -> gate (answer/clarify/decline) -> template or retrieval -> pack evidence -> grounded generation with ….

## Details

Gate first; serve common questions from templates. Pack evidence with structure (Tessera: +5-6 pts at same token budget). Check sufficiency (Certify: 80% with smallest sufficient set vs 57% with all passages). ….

## Sources

- [Tessera](https://arxiv.org/abs/2610.37080)
- [Certify](https://arxiv.org/abs/2610.34684)
- [claim smoothing](https://arxiv.org/abs/2610.35793)
