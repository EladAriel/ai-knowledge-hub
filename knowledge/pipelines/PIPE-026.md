# PIPE-026: Pipeline: end-to-end search plus a compiled wiki

## Summary

fake sources with permissions -> ingest -> keyword+vector index over raw docs -> nightly job writes a wiki that cites raw doc IDs -> agent gets search + wiki -> answer with citations or say it can't be done.

## Details

Raw docs stay source of truth; keep session-start memory small (index of a few hundred lines); test whole flow against a fixed fake dataset like Backlot per test user; give every safety filter two numbers (attacks caught + benign-case cost); make 'can't be done' / 'not allowed' valid finals. Owners: Architects (wiki↔raw tie, test users); Product (which questions justify the wiki, cost target); Devs (fake services in CI, nightly wiki job, regression diffs).

## Sources

- No external source link (in-house technique note).
