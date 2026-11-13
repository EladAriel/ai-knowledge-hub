# TOOL-045: Repos: NVIDIA/auto-ontology, EvoOntology, ontosmith

## Summary

A business ontology built from the database and served to agents over MCP, an ontology layer over MCP that keeps a change only if a before-and-after test shows it helps, and a design-the-ontology-first path into a Neo4j graph.

## Details

NVIDIA/auto-ontology builds a business ontology from your database's structure. It covers terms with synonyms, reviewed SQL measures, and how tables join. People approve the definitions, and agents use them through MCP, a command line or an API. Borrow: agents can't browse the raw database layout, so they have to use the approved definitions; a check that runs before answering, asking whether the question can be answered at all; approved corrections flow back into the ontology. Maturity: high, with 11.6k stars, pushed Nov 10, Apache-2.0, and Docker and Helm setups. Best for Architects, as a reference for who owns the ontology and how it's governed. ruc-datalab/EvoOntology is an ontology layer served over MCP, with plugins for Claude Code and Codex (paper arXiv 2609.15779). An agent drafts the ontology, then it improves from real usage. Each change is kept only if a before-and-after test shows it helps. Borrow: treat every ontology change like a database migration that needs a passing test. Maturity: medium, with 1.2k stars, pushed Nov 6, MIT; it comes from an academic lab, and the paper summary gives no headline numbers. Best for Devs, who can try it locally with the plugin. Dongbumlee/ontosmith has you design and approve the ontology first, then builds a knowledge graph from it in Neo4j. Cheap models suggest facts, and a stricter model checks each one against the source text; every fact keeps the exact text it came from; each build estimates its cost before spending anything. Borrow: a fixed list of entity types, each with a definition and edge-case examples, and no class hierarchy; separate models for suggesting facts and for checking them. Maturity: medium; 268 stars and pushed the same day, MIT, PyPI and CI, but it's about 3 weeks old with one maintainer. Best for Architects and Devs.

## Sources

- [NVIDIA/auto-ontology](https://github.com/NVIDIA/auto-ontology)
- [EvoOntology](https://github.com/ruc-datalab/EvoOntology)
- [EvoOntology paper](https://arxiv.org/abs/2609.15779)
- [ontosmith](https://github.com/Dongbumlee/ontosmith)
