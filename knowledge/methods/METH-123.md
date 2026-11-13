# METH-123: Hybrid search straight on the data lake (Apache Pinot and Iceberg)

## Summary

Keyword search, vector search and combining the two rankings all run as plain SQL on the main data table. There is no copy in a separate search engine and no sync job.

## Details

Results: quality matches exact search, and a new write becomes searchable in 3.8 seconds. Caveats: tested on e-commerce data; mostly a well-built combination of existing tools, not a new technique, but one system of record means no stale copies. Effort: high. Adopt for: Architects decide where the source of truth lives; Devs prototype the ranking combination as a SQL query and compare it with your current setup. arXiv 2611.11031.

## Sources

- [Pinot/Iceberg lake search (arXiv)](https://arxiv.org/abs/2611.11031)
