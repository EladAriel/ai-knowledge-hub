# TOOL-021: Repos: SpiceDB secure-RAG workshop, schemagate, VaultRAG

## Summary

Permission pre-filtering in a LangGraph+Qdrant RAG; access control for text-to-SQL; ACL check inside the same Postgres query.

## Details

authzed workshops/secure-rag-pipelines: prefilter_node.py asks SpiceDB for viewable doc IDs and passes them to Qdrant; shows post-filtering failing (contractor sees 7/50 docs, top-5 often empty); allowed_doc_ids: None = fail-open bug to test for. ashishsinha1602/schemagate (173, young, verify): ungranted tables never reach the prompt; Catalog.select(question, principal=...), max-age refusal. AgentPostmortem/VaultRAG (1 star, test pattern only): tests/test_acl.py 12 tests; with the check removed leaks 0% -> 81.8% while recall stayed 100%.

## Content

**[ashishsinha1602/schemagate](https://github.com/ashishsinha1602/schemagate)** adds access control to text-to-SQL. Tables the user hasn't been granted never reach the prompt, and it can read the database's own permission grants.
- What to borrow: `Catalog.select(question, principal=...)`, plus a max-age setting that refuses to answer when the table list can't be re-read.
- Maturity: it claims 65–79% fewer schema tokens in the prompt. 173 stars, Apache-2.0, pushed today. It's young and the ratio of stars to forks looks odd, so verify it before relying on it.
- Best for: Devs.

**[AgentPostmortem/VaultRAG](https://github.com/AgentPostmortem/VaultRAG)** runs the permission check inside the same Postgres query as the vector and keyword search, and denies access by default.
- What to borrow: `tests/test_acl.py`, 12 tests against a real database, such as "revoked access takes effect immediately" and "groups are never taken from the request."
- Its eval: it reports leak rate next to recall. With the permission check deleted, leaks went from 0% to 81.8% while recall stayed at 100%, so recall alone would never have caught it.
- Maturity: 1 star, MIT. It's here for the test pattern, not as a dependency.
- Best for: Devs.

## Sources

- [SpiceDB workshop](https://github.com/authzed/workshops/tree/main/secure-rag-pipelines)
- [schemagate](https://github.com/ashishsinha1602/schemagate)
- [VaultRAG](https://github.com/AgentPostmortem/VaultRAG)