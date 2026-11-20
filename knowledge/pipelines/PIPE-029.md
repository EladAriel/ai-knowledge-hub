# PIPE-029: Pipeline: indexing (hybrid index, compression tuned on your data, filter in-query)

## Summary

cleaned chunks -> keep the raw text for keyword search and an embedding for vector search -> one index holding keywords, vectors and metadata -> choose vector compression by testing on your own data -> apply filters and permissions inside the query -> combine the keyword and vector rankings (RRF) -> rerank the top 50–100

## Details

Make the index hybrid from day one. Adding keyword search (BM25) to a vector-only index later is painful. Combine the two rankings with reciprocal rank fusion (RRF). Leave its rank constant at the default of 60 until you have eval data (Dell and Elastic). Tune compression to your data instead of picking one setting. Elastic now picks how many bits to keep for each part of the index automatically; it stayed within 3 points of full-precision recall across 11 datasets (Elastic DiskBBQ). Extreme compression can work, but test it. On AWS, shrinking each vector number to 1 bit, then re-scoring the top results at full precision, cut a 100M-vector pgvector index from 367 GB to about 38 GB; it works with some embedding models and fails with others (AWS). Filter inside the query, not afterwards: filtering after search can quietly leave you with too few results; index nested fields per object. Re-index only files that changed, and treat a stale index as a bug. Owners: Architects set up one index per access boundary, with a written recall target for each and a named owner for the compression choice; Product decides how much recall you'll trade for lower cost, in dollars per month; Devs keep index settings in code and run a recall check in CI whenever they change. Added on Nov 12 (indexing stage, third time on it).

## Sources

- [Dell and Elastic on hybrid search](https://www.dell.com/en-us/blog/beyond-vectors-hybrid-search-for-enterprise-ai/)
- [Elastic DiskBBQ auto-calibration](https://www.elastic.co/search-labs/blog/diskbbq-quantization-bits-auto-calibration)
- [AWS binary quantization on Aurora](https://aws.amazon.com/blogs/database/scale-pgvector-with-binary-quantization-on-amazon-aurora-postgresql/)
