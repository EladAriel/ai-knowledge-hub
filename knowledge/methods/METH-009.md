# METH-009: Beyond the Final Embedding

## Summary

Memory retrieval that uses the token representations that the embedding model has already calculated.

## Content

**2. [Beyond the Final Embedding](https://arxiv.org/abs/2610.13277)**
- **What it is:** Memory retrieval that uses the token representations that the embedding model has already calculated. Each token in the query searches for matching tokens in memories, and the score is combined with the similarity of the entire memory.
- **Why new:** The idea is close to ColBERT style late interaction. The new thing is that it works without training, with the same encoder, and is aimed at call memory.
- **Evidence:**
  - According to the article there is an improvement in eight benchmarks.
  - With a small query adapter, on Qwen3-Embedding-4B: an improvement of 13.3 points in Recall@10 and 14.3 points in NDCG@10.
  - The results have not been reproduced by others and there is no code.
  - You should check how much it costs to store vectors at token level.
- **Scores:** Effectiveness 3.5/5, Hype 1/5.
- **Compatibility:** Long-term memory and RAG. **medium** effort.
- **Recommendation: Pilot**

## Sources

- [Beyond the Final Embedding](https://arxiv.org/abs/2610.13277)
