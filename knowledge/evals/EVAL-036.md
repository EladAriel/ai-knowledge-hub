# EVAL-036: Eval: parsing accuracy scorecard (facts kept, before any search)

## Summary

A small hand-labeled test of whether the parser kept the facts, before any search happens. New in the eval rotation on Nov 10.

## Details

Steps (under a day): pick 20–30 real documents (tables, multi-column pages, scans, slides); for each, write down 5–10 key facts with page numbers; run each parser you're comparing; score whether each fact was found, whether its value is right, and whether it's on the right page or page area; also log the share of chunks that got a vector and how many the embedding step rejected; run it in CI on every parser or chunking change and block the change if either score drops (Agile Monkeys). Catches broken tables, mixed-up columns, missing headings, chunks that quietly never got a vector, and problems after parser upgrades. Owners: Devs the CI job; Product the documents and facts; Architects the searchable-chunk target.

## Sources

- [Agile Monkeys](https://labs.theagilemonkeys.com/posts/what-we-learned-moving-retrieval-evals-into-the-ingestion-pipeline/)
