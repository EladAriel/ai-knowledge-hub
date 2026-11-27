# EVAL-045: Eval: enrichment stability test

## Summary

A half-day eval (Nov 22). Run your tagger twice, or with two models, on the same 50 chunks. For each field, such as type, owner, date or product, measure how often both runs agree. Fields that agree less than about 80% of the time aren't safe to use as search filters. Fix the prompt or drop the field.

## Details

What it catches: enrichment fields that look useful but flip from run to run, then silently break filters and facets.

Who runs it: Devs run the two passes and compute per-field agreement. Architects decide the agreement floor (about 80% is the suggested starting point) and which fields may be used as filters. Product reviews fields that have to be dropped.

Related: EVAL-017 is a labeled precision/recall spot-check of extracted entities, not a two-run agreement test. Complements the enrichment practice in PIPE-037.

Effort: half a day.

## Sources

- [PIPE-037: keep what the source said apart from what we concluded](../pipelines/PIPE-037.md)
- [raskell: building IT intelligence (background for PIPE-037)](https://raskell.io/articles/building-it-intelligence/)
