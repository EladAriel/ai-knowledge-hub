# METH-012: Keep Your Receipts (PolyGraph): Clearing knowledge graphs

## Summary

Each item in the knowledge graph that an agent builds is saved with a 'receipt', i.e. a record of the sources that support it.

## Content

### 5. [Keep Your Receipts (PolyGraph): Knowledge Graph Cleaning](https://arxiv.org/abs/2610.17719)
[code](https://github.com/VishiATChoudhary/polygraph)

- **What it is:** Each item in the knowledge graph that a build agent is saved with a "receipt", meaning a record of the sources that support it. When a source is deleted, it is possible to calculate what should be deleted without calls to the model.
- **Why new:** This is not a normal provenance. There is an audit that decides which layer in the graph can be trusted.
- **Evidence:** Receipts are reliable in mergers (68% to 85%), and fail in summaries (about a third). If you don't trust the summary layer, contaminated queries drop from 28%-37% to less than 1%, and almost without affecting recall. Checked on PubMed with really retracted articles.
- **Scores:** Effectiveness 4/5, Hype 2/5.
- **Adjustment and effort:** GraphRAG and agent memory whose sources are updated. **medium to high** effort.
- **Recommendation: Pilot**, if you need to delete sources  has built.

## Sources

- [Keep Your Receipts (PolyGraph): Clearing knowledge graphs](https://arxiv.org/abs/2610.17719)
- [code](https://github.com/VishiATChoudhary/polygraph)
