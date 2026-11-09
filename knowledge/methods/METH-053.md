# METH-053: Knowledge layer that organizes before it retrieves (scope-to-IDs first)

## Summary

Tag every artifact with producer/service/domain/type; resolve each query to artifact IDs first, then search only those.

## Content

**1. [A knowledge layer that organizes before it retrieves](https://arxiv.org/abs/2610.32851)** (arXiv, Oct 26)
- **The setup:** seven agents reverse-engineered 241 repos from 18 services. Plain vector search kept returning a nearly identical rule from the wrong service, ranked high, with nothing to show it was wrong.
- **The fix:** tag every artifact with its producer, service, domain and type. Each query is first turned into a set of artifact IDs, and only those IDs get searched. The wrong rule doesn't rank lower; it never shows up at all.
- **Caveat:** it helped find the root cause of more than 100 production defects, but there's no accuracy number against a baseline yet. It's basically metadata filtering before search, under a new name.
- Adopt for:
  - *Architects:* make producer, service and domain required metadata fields when data comes in.
  - *Product:* look for "answer came from the wrong team" complaints, since that's the failure this fixes.
  - *Devs:* resolve the scope to a list of IDs first, then pass it as the vector-search filter.

## Sources

- [arXiv 2610.32851](https://arxiv.org/abs/2610.32851)
