# METH-201: Decision Columns as an Index

## Summary

Dense embeddings can't explain why two records matched, and adding a new property means re-embedding everything. In this method, a record's vector is its yes / no / not-stated answers to a list of plain-language questions. Every match explains itself question by question. A new question adds a column without touching the old ones. Adding questions taken from failed searches tripled a standard ranking score, and it matched dense retrieval on product benchmarks. No code was found. Why it matters: it's worth a read if you need auditable entity matching, for example for parts or customers. Next step: read the paper if that matching problem is on your list. For: architects and product. arXiv 2611.27910.

## Details

Reported Nov 23.

## Sources

- [Decision Columns as an Index](https://arxiv.org/abs/2611.27910)
