# METH-098: FlashProve: Progress on provable inference (Anthropic)

## Summary

Proves that a response was produced by a specific committed model without revealing the weights. Open code (Apache 2.0) with Lean proofs of the security properties.

## Content

**5. [FlashProve: Progress on provable inference (Anthropic)](https://www.anthropic.com/research/provable-inference)** ([HN discussion](https://news.ycombinator.com/item?id=50368626), 210 points)
- **What it is:** Proves that an answer was produced by a specific signed model, without revealing the weights. Open source (Apache 2.0) and comes with Lean proofs for security features.
- **Why new:** In the field of zkML this is a leap of magnitudes. According to the post: Llama 4 Maverick (400B) is proven at about 110 tokens per second on a single H100, proof of about 19MB, and verification in about 17 seconds on CPU. Previous work on the same model reported 14.3 hours per 1,000 toucans.
- **Evidence:** Code and Lean published. Declared limitations: greedy decoding on complete builds only, the context up to 1,024 tokens, the architecture is not hidden, there is no formal guarantee that the fast code is Lean compatible.
- **Scores:** Effectiveness 2/5 for today's products, hype 2/5.
- **Compatibility:** Relevant when a provider or router may replace your model, and for products in a regulated area. It is currently a research prototype. **high** effort.
- **Recommendation: Watch**

## Sources

- [Anthropic FlashProve post](https://www.anthropic.com/research/provable-inference)
- [HN (210 points)](https://news.ycombinator.com/item?id=50368626)
- [FlashProve](https://github.com/anthropics/FlashProve)
