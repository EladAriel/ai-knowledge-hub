# TOOL-033: Repos: neo4j-labs/agent-memory, GLiNER2

## Summary

neo4j-labs/agent-memory: graph memory for agents (Python/TS SDKs) with three-way entity outcome (merge / pending-duplicate review / new). GLiNER2: small local CPU models (74M–287M) extracting entities, categories, records and relations against a schema in one pass.

## Content

**[neo4j-labs/agent-memory](https://github.com/neo4j-labs/agent-memory)** is graph memory for agents, with Python and TypeScript SDKs. Each extracted entity gets one of three outcomes: merged into an existing node, sent to a review queue as a pending duplicate, or created as a new node.
- What to borrow:
  - A different match threshold for each entity type, for example 0.95 for people and 0.88 for products.
  - A list of known aliases, like code names, tickers and product codes.
  - The `find_potential_duplicates()` and `review_duplicate()` review queue.
  - Recording the merge decision and its score on every node.
- Maturity: 599 stars, 109 forks, pushed Nov 1, Apache-2.0. It's a Neo4j Labs beta with no support or compatibility promises.
- To run it: `pip install 'neo4j-agent-memory[nams]==0.8.0'`, or self-host on Neo4j. It also runs as an MCP server through `uvx`. These steps come from the README; I didn't run them.
- Best for: Architects, for the resolution rules, and Devs, including TypeScript and Vercel AI SDK users.

**[fastino-ai/GLiNER2](https://github.com/fastino-ai/GLiNER2)** offers small local models (74M–287M parameters, built for CPU). In one pass they pull entities, categories, structured records and relations from text, following a schema you give them.
- [GLiNER2.5](https://fastino.ai/blog/gliner2-5-span-free-information-extraction) shipped Aug 24. It removes the limit on how long an entity can be and keeps each entity's exact position in the source.
- What to borrow:
  - A cheap first pass before any LLM call, so the LLM only handles what's left.
  - Tagging restricted to a fixed list of labels.
  - A multilingual model (`gliner2.5-multi-v1`). Test Hebrew yourself, since the README doesn't confirm it.
- Maturity: 2,433 stars, 218 forks, pushed Oct 20, Apache-2.0.
- To run it: `pip install gliner2[local]`. This comes from the README; I didn't run it.
- Best for: Devs.

## Sources

- [neo4j-labs/agent-memory](https://github.com/neo4j-labs/agent-memory)
- [fastino-ai/GLiNER2](https://github.com/fastino-ai/GLiNER2)
- [GLiNER2.5 blog](https://fastino.ai/blog/gliner2-5-span-free-information-extraction)
