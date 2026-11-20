# TOOL-048: Repos: lightonai/next-plaid, terrierteam/ir_measures

## Summary

A search engine that stores several vectors per document (ColBERT-style), including a local ColGREP tool for code; and one Python API for standard search metrics, with a per-query score you can group by source.

## Details

lightonai/next-plaid stores several vectors per document instead of one. It includes ColGREP, a local command-line tool for code that combines regex filters with semantic ranking. ColGREP works with Claude Code, Codex and OpenCode. Borrow: regex filtering followed by semantic ranking; one index per project and embedding model, so switching models is safe; an easy local test of several vectors versus one on your own code. Maturity: medium to high, with 617 stars, Apache-2.0, release 1.8.5 on Oct 10, and about 760 commits. Best for Devs. terrierteam/ir_measures is one Python API for the standard search metrics, like recall, nDCG and reciprocal rank (docs at ir-measur.es). Borrow: its iter_calc gives a score for each query, which you can then group by data source, user type or question type. Maturity: high. It's from the Glasgow Terrier team, with Apache-2.0, CI tests and commits on Oct 20. It has only 104 stars, but it's a standard tool in search research. Best for Devs running evals in CI, with Product reading the breakdowns. vespa-engine/sample-apps rag-blueprint, covered the same day, is described in TOOL-034.

## Sources

- [lightonai/next-plaid](https://github.com/lightonai/next-plaid)
- [terrierteam/ir_measures](https://github.com/terrierteam/ir_measures)
- [ir_measures docs](https://ir-measur.es/)
