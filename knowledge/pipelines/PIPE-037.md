# PIPE-037: Pipeline: enrichment — keep what the source said apart from what we concluded

## Summary

Enrichment angle (Nov 22): keep "what the source said" apart from "what we concluded." Save raw source facts and inferred entities separately. Store every inferred link as a row with its basis, a confidence score and the source. Match identities in order: shared keys first, then rules, then the model. Low-confidence links go to the owning team to confirm. That way you can undo a bad merge without re-ingesting everything.

## Details

Based on raskell's early open reference build from Nov 16 (Go, Apache-2.0). This differs from earlier enrichment angles (PIPE-010, PIPE-019, PIPE-028), which were about extraction and entity-resolution patterns. Today's practice is the bookkeeping: observations stay separate from inferences, every inferred link keeps its basis and confidence, and identity matching has a fixed order.

Who owns it: Architects define the observation-versus-entity split and the matching order. Devs store the basis and confidence on every inferred link. Product and the owning team confirm low-confidence links.

See also EVAL-045 (enrichment stability test).

## Sources

- [raskell: building IT intelligence (Nov 16)](https://raskell.io/articles/building-it-intelligence/)
