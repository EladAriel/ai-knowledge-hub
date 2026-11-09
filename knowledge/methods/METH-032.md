# METH-032: The bottleneck is retrieval, not reading

## Summary

Similarity search finds a relevant chunk but often misses all chunks a multi-fact question needs; chunking strips doc identity.

## Details

Scoring answers together with line-level citations exposes grounding failures that answer-only scoring hides. Make doc-level metadata (title, version, owner) required on every chunk; add a short doc header to each chunk before embedding; tag golden questions single- vs multi-fact and report separately.

## Content

**4. [The Bottleneck Is Retrieval, Not Reading](https://arxiv.org/abs/2610.26951)** (arXiv, Oct 18)
- **Finding:** similarity search reliably finds *a* relevant chunk, but it often misses *all* the chunks a multi-fact question needs.
- **Second problem:** chunking strips out which document a chunk came from (which paper, which version), so "what did doc X say" questions fail.
- **On evals:** scoring the answer together with line-level citations exposes grounding failures that scoring the answer alone hides.
- Adopt for:
  - *Architects:* make doc-level metadata (title, version, owner) a required part of every chunk.
  - *Product:* tag golden questions as single-fact or multi-fact and report them separately.
  - *Devs:* add a short doc header to each chunk before embedding it.

## Sources

- [The Bottleneck Is Retrieval, Not Reading](https://arxiv.org/abs/2610.26951)