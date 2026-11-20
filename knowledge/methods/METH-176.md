# METH-176: New terms (Nov 18, enterprise knowledge): contamination@5, value-agnostic query, documentation drift, gap rate, fault-owner, noise band, withdraw/re-earn, shadow mode

## Summary

One-line terms (Nov 18) on the feedback and monitoring stage.

## Details

contamination@5: how often a stale (superseded) version of a fact appears in the top 5, which can hide behind a correct top result (StaleBench). Value-agnostic query: a "what is X now?" question that names the entity but not the value, so every stored version matches equally well. Documentation drift: docs falling behind shipped code or behavior, found via tickets and code-doc mismatches (Mind the Gap). Content / customer-data / action gap: separates "the AI didn't know" from "the AI couldn't reach the data" from "the AI couldn't do it"; each needs a different fix (Intercom Fin's grouping as described in a third-party comparison; Intercom's own doc lists missing, unclear, duplicate or contradictory content). Gap rate and time-to-close: failed-query clusters per 1,000 questions, and the median days from opening a gap to verifying its fix. Fault-owner taxonomy: labels each failure by the layer whose owner fixes it (instructions / tools / model / data), fixed before analysis starts. Run-to-run noise band: the score and cost spread across N identical runs; changes smaller than this are not improvements. Withdraw / re-earn: a learned semantic rule is removed when later outcomes contradict it, and can come back after new verified successes (LCG). Shadow mode: the agent proposes fixes next to people without shipping them, until you know how often they're accepted.

Recurring themes: production signals as the eval source (Uber/Arize, Mind the Gap, LCG, Ratel); measure noise before claiming gains, including LoCoMo scores moving up to 9.3 points from prompt or judge choice alone (arXiv 2611.19199); freshness and supersession as first-class, carried over from raw-beats-summaries and memory audits; authorization stays outside the model (OWASP-mapped framework tests, 2611.21259, seen but not used as a full item).

## Sources

- [LoCoMo score movement (theme)](https://arxiv.org/abs/2611.19199)
