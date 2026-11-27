# EVAL-044: Eval: re-sync churn test

## Summary

A same-day eval you can start in under a day (Nov 20). Sync one source twice from an unchanged copy, then run one update-only sync. Count new, changed and re-embedded chunks, and check whether the number of docs changed. Every count should be 0. Anything above 0 means wasted embedding money or duplicates in the index. Track it for each connector in your CI.

## Details

What it catches: connectors that re-embed unchanged documents, or that leave deleted docs in the index. A document-count change after an unchanged re-sync is a bug, not a refresh.

Start in under a day: pick one source, sync it twice from an unchanged copy, run one update-only sync, and record the four counts (new chunks, changed chunks, re-embedded chunks, document-count change).

Who runs it: Devs add the counts to CI for each connector. Architects decide what a deletion record looks like. Product watches wasted embedding cost.

Related: EVAL-030 already checks that running a sync twice creates no extra copies. This eval adds the update-only pass and the re-embedded and document-count checks. Complements the ingestion practice in PIPE-035.

Effort: under a day.

## Sources

- [PIPE-035: make every sync safe to repeat](../pipelines/PIPE-035.md)
- [EVAL-030: duplicate crowding and repeat syncs](EVAL-030.md)
