# PIPE-013: Pipeline: retrieval + calibrated reranking

## Summary

query -> optional rewrite -> permission-filtered BM25 + vector (top 50-100 each) -> RRF -> cross-encoder rerank -> keep above calibrated threshold or 'I don't know' -> pick passages -> answer.

## Details

Choose candidate depth by measured candidate recall on the golden set. Don't threshold merged scores (RRF tops out at 2/61 with two retrievers; min-max makes the best weak match 1.0). Threshold only the reranker score, stored with model version, rechecked as corpus grows. In agent loops give the reranker the original task too. Keep permission filter before reranking; log each doc's rank at every stage. Eval: stage ablation test (five setups turning stages on one at a time; candidate recall, gains, p95 latency per stage; CI fails if a stage's gain drops below margin).

## Content

## Pipeline pattern of the day: retrieval and reranking

query -> optional rewrite -> keyword (BM25) and vector search in parallel, filtered by permissions, top 50–100 each -> merge with RRF -> cross-encoder rerank -> keep docs above a calibrated threshold, or say "I don't know" -> pick the relevant passages -> answer layer

- **Retrieve wide, then rerank narrow.** Choose how many candidates go to the reranker by measuring, on your golden set, how often the right doc is among them, not by gut feel.
- **Don't set a threshold on merged search scores.** An [AWS write-up](https://builder.aws.com/content/3KJyvPGmUnCxmFR0gG2wGkHoYTR/hybrid-search-and-reranking-what-each-one-actually-buys-you) explains why:
  - RRF (reciprocal rank fusion) scores only reflect each doc's position in the lists, and top out at 2/61 with two retrievers.
  - Rescaling scores to 0–1 makes the best weak match look like a perfect 1.0.
  - The post says it didn't measure how much this matters in practice, so measure it on your own data.
- **Set a threshold only on the reranker's score.** Store it with the model version, and recheck it as the corpus grows.
- **In agent loops, give the reranker the original task** as well as the sub-query.
- **Keep the permission filter before reranking,** as in yesterday's brief. Log each doc's rank at every stage, so you can see which stage lost the right answer.
- **Who owns it:**
  - *Architects* own the interface between stages (candidate count, what a score means, and the "I don't know" signal), and decide whether the reranker runs as an outside API or inside your own network.
  - *Product* owns the trade-off between quality, latency and cost, and the "I don't know" experience.
  - *Devs* own the settings (k values, the RRF constant of 60, the threshold), logging at each stage, and the CI eval below.

## Sources

- [AWS hybrid search write-up](https://builder.aws.com/content/3KJyvPGmUnCxmFR0gG2wGkHoYTR/hybrid-search-and-reranking-what-each-one-actually-buys-you)