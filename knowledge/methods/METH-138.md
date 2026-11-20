# METH-138: Qdrant 1.20: smaller vectors and filters on nested data

## Summary

A vendor post (benchmark code linked) on Qdrant 1.20. New vector formats take a quarter or half the space of full-precision vectors; speed stays within 10% of full precision, with no extra re-scoring step. Nested filters are about filtering on lists of objects, like a list of authors, each with a first and last name.

## Details

Plain filters missed between a fifth and a third of the right papers. A new index that checks each object separately returned correct results and handled up to 4 times more queries per second. Effort: low. Adopt for: Architects—mark nested metadata, like owners, permission groups and tags, as a correctness risk in the data contract; Product—to users, wrong filter results look like a bad AI, so test them; Devs—add a nested-filter test for every filter on a list of objects. Related earlier item: TOOL-034 (Qdrant / Vespa / pgvectorscale, including Qdrant v1.20.0 for named-vector migrations).

## Sources

- [Qdrant 1.20 performance (vendor post)](https://qdrant.tech/blog/qdrant-1.20-performance/)
