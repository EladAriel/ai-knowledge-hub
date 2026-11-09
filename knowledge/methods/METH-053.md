# METH-053: Knowledge layer that organizes before it retrieves (scope-to-IDs first)

## Summary

Tag every artifact with producer/service/domain/type; resolve each query to artifact IDs first, then search only those.

## Details

Seven agents reverse-engineering 241 repos from 18 services: plain vector search kept returning a near-identical rule from the wrong service. With scope-first, the wrong rule never shows up. ….

## Sources

- [arXiv 2610.32851](https://arxiv.org/abs/2610.32851)
