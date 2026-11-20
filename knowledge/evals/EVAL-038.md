# EVAL-038: Eval: compression budget test

## Summary

Finding the cheapest index setup that keeps answers as good as full precision. One script over your existing golden set; rerun it whenever you change embedding models. Added on Nov 12.

## Details

Steps (under a day): 1. Take 200–1,000 real queries plus your golden questions. 2. Find the true nearest neighbours for each query by checking every vector, with no index. 3. Try several setups: full precision, half precision, 8-bit, 4-bit and 1-bit, each with and without re-scoring. For each, log recall against the true neighbours and on your golden questions, memory and disk use, and p95 latency (95% of queries are faster than this). 4. Pick the smallest setup whose recall drops no more than you agreed, for example 1–2 points. 5. Add one nested-filter check: run the same filter both ways and count wrong results. What it catches: embedding models that don't survive compression, too little re-scoring, and filters that return wrong rows. Who runs it: Devs build it and run it in CI; Architects set the allowed recall drop; Product signs off on the cost versus the recall drop.

Effort: under a day.

## Sources

- No external link was recorded for this eval itself. Related public sources (see PIPE-029):
- [Elastic DiskBBQ auto-calibration](https://www.elastic.co/search-labs/blog/diskbbq-quantization-bits-auto-calibration)
- [AWS binary quantization on Aurora](https://aws.amazon.com/blogs/database/scale-pgvector-with-binary-quantization-on-amazon-aurora-postgresql/)
- [Qdrant 1.20 performance (vendor post)](https://qdrant.tech/blog/qdrant-1.20-performance/)
