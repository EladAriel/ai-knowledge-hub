# METH-188: Microsoft Foundry IQ: permission-aware SharePoint, cited graphs, and GraphRAG Zero

## Summary

Microsoft Foundry IQ is the big-vendor version of the ontology-plus-permissions-plus-cited-graph design that keeps coming up. While indexing, it maps entities to your ontology or to a graph you bring, and every link keeps its source. You can ask in plain language or in a graph query language. Answers based on SharePoint now respect each user's and group's permissions (that part is generally available). A small preview model plans the searches. Copy one rule: when a policy can't be checked, access is denied. This is a vendor blog with no comparison numbers, and partly just a new name for an enterprise context layer. For: architects.

## Details

Reported Nov 20, with a Nov 22 follow-up on GraphRAG Zero, now inside Foundry IQ.

The problem Foundry IQ is aimed at: agents search the same docs over and over to piece facts together, and they often see more than the user is allowed to. Related: METH-147 (Databricks Genie Ontology).

Nov 22 update — GraphRAG Zero: classic GraphRAG is too slow and expensive to keep up to date on live company data. Here the graph is built from embeddings only, with no model calls at index time, and optionally none at query time. In Microsoft's own test of 200 synthetic questions, coverage of facts needed for a full answer rose from 53.4% to 57.4% versus plain vector search, and context was ready in 0.93 seconds. Vector search still picked more precise chunks. That's a modest gain, and no open-source library is named. Why it matters: connected context can now be cheap enough to rebuild whenever the data changes. Next step: steal their eval idea. Score retrieved chunks against fact claims as full (1), partial (0.5) or none (0), not just the final answer. For: architects.

## Sources

- [Foundry IQ knowledge graphs and permission-aware SharePoint](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/foundry-iq-introducing-knowledge-graphs-engineered-for-agents/4572683)
- [GraphRAG Zero (Microsoft Research)](https://www.microsoft.com/en-us/research/story/the-evolution-of-graphrag-advancing-systems-and-evaluation-together/)
