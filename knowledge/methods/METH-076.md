# METH-076: FalkorDB: entity resolution at scale in GraphRAG-SDK

## Summary

After each batch, finalize checks only the new entities (rest of the item was cut off in the transcript). Pipeline guidance from the same brief: give the judge identifying properties, not metadata; check new entities against the whole graph; keep the losing values as history and aliases searchable.

## Details

From the brief's pipeline section citing FalkorDB: give the merge judge identifying properties (e.g. birth year, ticker, employee ID) rather than metadata; check new entities against the whole graph; when merging keep the losing values as history and keep aliases searchable. (Full insight text was truncated in the available transcript.).

## Sources

- [FalkorDB entity resolution blog](https://www.falkordb.com/blog/knowledge-graph-entity-resolution/)
