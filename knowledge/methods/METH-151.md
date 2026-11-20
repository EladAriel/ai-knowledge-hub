# METH-151: RetailBridge: combining tables and text is the real bottleneck

## Summary

A 1,680-question benchmark that needs evidence from both tables (orders, products) and text (reviews, customer questions). Their agent first gets a short description of the tables, plans which source each step uses, and repairs failed steps one at a time. Effort: medium. Accepted at KDD 2027.

## Details

Results (arXiv 2610.25096): 0.429 accuracy, scored by an LLM judge, using 7.45 API calls per question. The baseline scored 0.293 using 25.21 calls. Across 10 LLMs, combining evidence from different sources was the main failure. Limits: synthetic retail data, an LLM judge, and the repo is still empty. Rebrand watch: this is text-to-SQL plus RAG with a router, done carefully. Adopt for: Architects give agents a short, stable description of the data. Include the tables, their keys, and which (the source note was cut off after this phrase, so the remaining adopt bullets are missing).

## Sources

- [RetailBridge / RetailRAG](https://arxiv.org/abs/2610.25096)
