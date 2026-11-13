# METH-124: Search-by-answer bias in vector retrievers (Goldberg lab)

## Summary

Across 8 retrievers, including E5 and Qwen3-Embedding, passages that mention the answer the model already 'expects' rank higher, even when the passage states the wrong relationship.

## Details

Why it matters: internal facts that differ from common public knowledge can get pushed down, like your own pricing, org chart or product names. Keyword search helps here. Effort: low to act on. Adopt for: Architects require hybrid search for fact lookups; Product list 'facts that contradict public knowledge' as a known risk; Devs add golden questions whose right answer goes against public knowledge. arXiv 2611.11396.

## Sources

- [Search-by-answer bias (arXiv)](https://arxiv.org/abs/2611.11396)
