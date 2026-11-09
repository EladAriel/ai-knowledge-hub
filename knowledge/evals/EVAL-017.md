# EVAL-017: Eval: extraction spot-check with drift rates

## Summary

Precision/recall of extracted entities vs a small hand-labeled set, plus over-count, grounding, duplicate and deletion rates.

## Details

1) Sample 50 chunks incl. 0-1 entity, mixed Hebrew/English names, tables. 2) Label once (~2 h). 3) Precision/recall per entity type. 4) Over-count rate, grounding rate (values pointing to source position), duplicate rate, deletion check (delete 3 docs, confirm facts gone). 5) CI fails if any number drops >5 points.

## Content

## Simple eval technique: extraction spot-check

**What it is:** you measure the precision and recall of extracted entities and fields against a small hand-labeled set. Then you add four rates that show when enrichment starts to drift.

**Steps (under a day):**
1. Sample 50 chunks. Include some with zero or one entity, a few with mixed Hebrew/English names, and a few tables.
2. Have someone label the true entities and fields once, which takes about 2 hours in a spreadsheet.
3. Run the extractor, and compute precision and recall for each entity type.
4. Add four rates:
   - Over-count rate: how often the extractor returns more items than are really there.
   - Grounding rate: the share of values that point back to a position in the source.
   - Duplicate rate: how often one real entity is stored as two.
   - Deletion check: delete 3 docs and confirm none of their facts come back.
5. Save it as a CI test that fails if any number drops by more than 5 points.

**What it catches:** padded lists, invented entities, schema drift after prompt or model changes, duplicates of the same name in different scripts, and facts that survive their source's deletion.

**Who runs it:** Devs own the CI test. Product owns the labeled set and its thresholds. Architects review the duplicate and deletion numbers as governance signals.