# METH-142: Apple SupportNet and KeyNet: faster vector search

## Summary

Small networks are trained offline on a fixed collection. SupportNet routes each query to the right cluster. KeyNet predicts the best-matching vector directly and feeds it into an existing IVF index.

## Details

What's new: a new theoretical angle, not a rebrand. Searching for the largest inner product is in fact a convex function of a certain kind, so it can be learned with a network built for convex functions. Evidence: the paper was presented at ICML 2026. On Natural Questions (2.6 million passages) Apple reports 95% recall 1.9 times faster than routing by cluster centroids, and 99% recall with up to 8 times lower latency. These are Apple's own results. The method assumes a fixed collection and a stable query distribution. 201 points on HN. Scores: effectiveness 3/5, hype 2/5. Fit: relevant only at large scale with a stable collection; in most RAG products this is not the bottleneck. Effort: high. Recommendation: Watch. Source: machinelearning.apple.com/research/faster-retrieval.

## Sources

- [Apple SupportNet and KeyNet](https://machinelearning.apple.com/research/faster-retrieval)
