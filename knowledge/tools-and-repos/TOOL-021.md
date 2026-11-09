# TOOL-021: Repos: SpiceDB secure-RAG workshop, schemagate, VaultRAG

## Summary

Permission pre-filtering in a LangGraph+Qdrant RAG; access control for text-to-SQL; ….

## Details

authzed workshops/secure-rag-pipelines: prefilter_node.py asks SpiceDB for viewable doc IDs and passes them to Qdrant; shows post-filtering failing (contractor sees 7/50 docs, top-5 often empty); ….

## Sources

- [SpiceDB workshop](https://github.com/authzed/workshops/tree/main/secure-rag-pipelines)
- [schemagate](https://github.com/ashishsinha1602/schemagate)
- [VaultRAG](https://github.com/AgentPostmortem/VaultRAG)
