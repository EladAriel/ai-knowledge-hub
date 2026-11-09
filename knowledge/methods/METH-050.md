# METH-050: Lychee: certified screening for high-recall GPU vector search

## Summary

GPU vector index 9.7-117x faster than cuVS IVF-Flat at the same recall.

## Details

Searches up to 1 billion vectors (rest of item elided in the transcript).

## Content

**2. [Lychee: certified screening for high-recall vector search](https://arxiv.org/abs/2610.30697)**
- **What it is:** a GPU vector index that's 9.7–117× faster than NVIDIA's cuVS IVF-Flat at the same recall, and searches 1 billion vecto...hold, for example 85%. Anything below that, plus every deletion, becomes a change request for a data steward. "Context sets" are permission-controlled slices per domain. The "4x more accurate" claim comes from Google's internal benchmarks only.
- **Rebrand watch:** this is a data catalog plus a business glossary plus a feedback loop. It's part of the same vendor wave as the Neo4j Context Engine (Oct 20) and the [Salesforce Agent Context Engine](https://www.salesforce.com/blog/agent-context-engine-trusted-shared-context/).
- Adopt for:
  - *Architects:* copy the pattern even without Google. The system proposes changes, a confidence threshold decides which need review, and every change goes in a log you can undo.
  - *Product:* show "users rephrasing the same question" on your dashboard as a sign of a knowledge gap.
  - *Devs:* store every generated definition with its citations, confidence and an `approved_by` field.

## Sources

- [Lychee](https://arxiv.org/abs/2610.30697)
- [Salesforce Agent Context Engine](https://www.salesforce.com/blog/agent-context-engine-trusted-shared-context/)