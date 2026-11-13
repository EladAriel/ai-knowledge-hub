# METH-122: NIFT-SQL: finding the right tables for enterprise text-to-SQL

## Summary

Fine-tunes a retriever and a small scoring model (560M) on each customer's example questions. The model scores whether a question needs each table, using only table names, column names and keys.

## Details

Results: across 244–971 tables, every needed table made the top 15 for 69–90% of questions, versus 22–41% for plain hybrid search. Why it matters: structured data needs its own retrieval layer, and a few labeled questions per customer go a long way. Effort: medium to high. Adopt for: Architects treat the list of tables and columns as an indexed source with an owner; Devs start with the version that needs no labels, then add fine-tuning. arXiv 2611.12731.

## Sources

- [NIFT-SQL (arXiv)](https://arxiv.org/abs/2611.12731)
