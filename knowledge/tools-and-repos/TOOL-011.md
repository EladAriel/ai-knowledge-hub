# TOOL-011: Repos: AWS context-ontology-accelerator, OmniGraph, PipesHub

## Summary

Ontology business-context layer over MCP/REST/SPARQL; graph DB on object storage with git-style branches; self-hosted workplace search.

## Content

**[aws/context-ontology-accelerator](https://github.com/aws/context-ontology-accelerator)** ([docs](https://aws.github.io/context-ontology-accelerator/)) is an open-source layer that gives agents business context. It works in three steps: it connects to your sources, an LLM proposes an ontology that a person reviews, and it serves context to agents over MCP, REST, or SPARQL.
- What to borrow:
  - Tiered answering: governed metrics first, then a query against the ontology, then a free-form agent as the fallback.
  - Permissions written in Cedar, AWS's open-source policy language.
  - Separate roles for data stewards and analysts.
- Maturity: about 990 stars and 128 forks, Apache-2.0, v0.3.6 released Oct 15, last pushed yesterday. It's heavy to run (AWS CDK, Java, and the Neptune graph database).
- Best for: Architects.

**[ModernRelay/omnigraph](https://github.com/ModernRelay/omnigraph)** ([cookbooks, including a company-brain starter graph](https://github.com/ModernRelay/omnigraph-cookbooks)) is a graph database that stores its data in object storage, using the Lance format. One query can combine vector, BM25 keyword, and graph search over typed data. It also has git-style branches and merges, so agents propose changes instead of writing straight to the main graph.
- What to borrow:
  - A branch per agent or task, merged after review.
  - `cluster plan` and `apply` commands that work like Terraform.
  - Cedar permission checks on every write.
- Maturity: about 1.5k stars and 235 forks, MIT, written in Rust, last pushed today. The managed cloud version is still waitlist-only.
- Best for: Devs.

**[pipeshub-ai/pipeshub-ai](https://github.com/pipeshub-ai/pipeshub-ai)** is self-hosted workplace search that also feeds context to agents. It has 50+ connectors and gives cited answers. Permissions are checked against each source system at query time. Agents connect as a specific person with that person's token, over MCP or ... does the same job as Onyx from Saturday's brief, so compare the two before picking one.
- Best for: Product, since it's the fastest way to demo a working company brain on real data.

## Sources

- [context-ontology-accelerator](https://github.com/aws/context-ontology-accelerator)
- [omnigraph](https://github.com/ModernRelay/omnigraph)
- [pipeshub-ai](https://github.com/pipeshub-ai/pipeshub-ai)
- [docs](https://aws.github.io/context-ontology-accelerator/)
- [cookbooks, including a company-brain starter graph](https://github.com/ModernRelay/omnigraph-cookbooks)
