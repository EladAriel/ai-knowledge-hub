# TOOL-033: Repos: neo4j-labs/agent-memory, GLiNER2

## Summary

neo4j-labs/agent-memory: graph memory for agents (Python/TS SDKs) with three-way entity outcome (merge / pending-duplicate review / new). GLiNER2: small local CPU models (74M–287M) extracting entities, categories, records and relations against a schema in one pass.

## Details

agent-memory — borrow: per-entity-type match thresholds (e.g. 0.95 people, 0.88 products); alias list (code names, tickers, product codes); find_potential_duplicates() + review_duplicate() review queue; record merge decision and score on every node. Maturity: 599 stars, 109 forks, pushed Nov 1, Apache-2.0, Neo4j Labs beta (no support promises). Run: pip install 'neo4j-agent-memory[nams]==0.8.0' or self-host on Neo4j; MCP server via uvx (from README, not run). Best for Architects (resolution rules) and Devs incl. TS / Vercel AI SDK.

## Sources

- [neo4j-labs/agent-memory](https://github.com/neo4j-labs/agent-memory)
- [fastino-ai/GLiNER2](https://github.com/fastino-ai/GLiNER2)
- [GLiNER2.5 blog](https://fastino.ai/blog/gliner2-5-span-free-information-extraction)
