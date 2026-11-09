# EVAL-025: Eval: old vs new index diff test (gate for an index/model switch)

## Summary

Run the same queries on the old (v1) and new (v2) index, label only the queries where they disagree, and allow the switch only if golden recall, win rate and threshold pass-rate all hold.

## Details

Note: the first steps of this eval were cut off in the available transcript; only the following parts are recorded. Step 5 (partial): check how many queries clear your score threshold on each index. 6) Allow the switch only if: golden recall is no worse; v2 wins or ties at least 60% of the labeled queries (choose your own bar); the share of queries clearing the threshold stays within a set range. Catches: quiet drops on exact-match queries (IDs, acronyms); score thresholds that no longer fit; an unfinished backfill (empty or short result lists); filter/access-control fields lost in the migration. Who runs it: Devs in CI on every index or model change; Product labels the disagreeing queries (diff-only labeling); Architects set the bar and require it for every new index version.

## Sources

- (no public source link recorded)
