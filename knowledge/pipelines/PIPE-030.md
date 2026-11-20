# PIPE-030: Pipeline: permissions and access control (two identities, filter before the model, overfetch or allow-list, deny on error)

## Summary

request with the user's and the agent's identity -> rough filter in the index by customer and data classification -> fetch several times more chunks than you need -> check each chunk's permission with fixed code, or filter by a list of allowed IDs -> keep the top results, and deny on any error -> rerank and answer with the LLM -> log who asked and which chunks were read

## Details

Every call carries two identities. The agent's identity says who ran it, and the user's says what it may read. Check permissions against the user (SynOS). Filter before any model reads content, including the reranker and the LLM. In the Authorization-First Retrieval paper, fetching first and filtering after showed unauthorized content in 86.1% of queries. Filtering after fetching can leave too few results, so fetch extra. If a user can only see a small share of documents, filter by their list of allowed IDs inside the query instead. Two limits apply (Elastic): listing everything a user can see in SpiceDB gets expensive above about 10,000 documents, and Elasticsearch caps that kind of ID filter at 65,536 values by default. Sync permissions from the systems that own them, like HR, your identity provider and the document systems. Removing access should be a delete, not a re-index. Deny on any error or missing permission, and log which passages each run read and for whom. Owners: Architects own the permission model and the sync from the identity, HR and document systems, and decide when to switch from fetching extra to filtering by allowed IDs; Product designs the screen a user sees when nothing is allowed, and tracks how often low-access users get an answer; Devs keep one authorize node the agent can't skip, and make the permission-model tests a CI step (see EVAL-039). Added on Nov 13 (permissions and access control stage).

## Sources

- [SynOS: permission-aware retrieval](https://www.getsynos.ai/blog/permission-aware-retrieval-ai-agents)
- [Authorization-First Retrieval](https://aclanthology.org/2026.trustnlp-main.15/)
- [Elastic: RAG with SpiceDB](https://www.elastic.co/search-labs/blog/fine-grained-authorization-elasticsearch-rag-spicedb)
