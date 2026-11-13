# EVAL-037: Eval: merge audit for entity resolution

## Summary

A check on whether you joined the right records. The Oct 24 check asked whether entities were found at all. This one asks whether matches were merged correctly. New in the eval rotation on Nov 11.

## Details

Steps (under a day): 1. Sample 200 candidate pairs, spread across auto-merged, sent to review, and marked new. Label each as same or different, which takes 2–3 hours. 2. Check the shortlist step: what share of the true matches made it onto the shortlist? 3. For each group, count wrong merges and missed merges separately. Wrong merges are worse, because they mix two customers' data. 4. Check what share of all errors falls in the review group. If most do, review is worth its cost. 5. Add the labeled pairs to CI and fail the build if wrong merges go up. What it catches: wrong merges that mix one entity's facts into another (which can also leak data across permission boundaries); duplicate entities that split answers in two; match thresholds that drift after an embedding-model change; shortlists that quietly miss true matches. Who runs it: Devs build it and gate CI on it; Product owns the labeling and decides how much worse a wrong merge is than a missed one; Architects set merge rules, for example no automatic merges across tenants or permission scopes.

## Sources

- No external source link (in-house technique note).
