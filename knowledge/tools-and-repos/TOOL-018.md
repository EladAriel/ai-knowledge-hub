# TOOL-018: Amazon OpenSearch intelligent ingestion

## Summary

Managed S3 -> index pipeline: layout-aware parsing, image captions via vision model, chunk, embed, index; jobs or streams.

## Content

**4. [Amazon OpenSearch intelligent ingestion](https://aws.amazon.com/blogs/big-data/build-rag-ready-indexes-from-amazon-s3-with-amazon-opensearch-intelligent-ingestion/)** (Oct 23)
- **What it does:** a managed pipeline from S3 files to a search index. It parses files while keeping layout and tables, uses a vision model to describe images in text, then chunks, embeds and indexes. Ingestion Jobs run once or on a schedule for backfills, and Ingestion Streams run continuously.
- **Why it matters:** it saves AWS teams weeks of pipeline work. The tradeoff is less control over chunking and source tracking. Check how document permissions carry over before adopting it, since the launch post focuses on parsing and embedding.
- Adopt for:
  - *Architects:* use it for low-risk document sets first, and keep your own pipeline where ACLs or source tracking are strict.
  - *Product:* use it to stand up a pilot fast.
  - *Devs:* run today's recall audit on its output before trusting it.

## Sources

- [AWS blog](https://aws.amazon.com/blogs/big-data/build-rag-ready-indexes-from-amazon-s3-with-amazon-opensearch-intelligent-ingestion/)
