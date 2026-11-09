# METH-098: FlashProve: Progress on provable inference (Anthropic)

## Summary

Proves that a response was produced by a specific committed model without revealing the weights. Open code (Apache 2.0) with Lean proofs of the security properties.

## Details

Per the post: Llama 4 Maverick (400B) proven at ~110 tokens/s on a single H100, proof ~19MB, verify ~17s on CPU; prior work on the same model reported 14.3 hours per 1,000 tokens. Declared limits: greedy decoding on an integer build only, context up to 1,024 tokens, architecture not hidden, no formal promise that the fast code matches the Lean. Scores: effectiveness 2/5 for products today, hype 2/5. Fit: relevant when a vendor or router may have swapped your model, and for regulated products; still a research prototype. Effort: high. Recommendation: Watch.

## Sources

- [Anthropic FlashProve post](https://www.anthropic.com/research/provable-inference)
- [HN (210 points)](https://news.ycombinator.com/item?id=50368626)
- [FlashProve](https://github.com/anthropics/FlashProve)
