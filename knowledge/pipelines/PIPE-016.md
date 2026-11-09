# PIPE-016: Pipeline: end-to-end with question-type routing

## Summary

sources -> permission-carrying incremental connectors -> parse + contextualize -> entity IDs + version links -> keyword/vector/graph index (links keep source IDs) -> permission filter -> route: lookups to hybrid+rerank, multi-source to wiki/graph, counting to SQL -> cited answer or decline -> feedback to eval set.

## Details

Match names to IDs before retrieval (EDGAR paper). Keep source record IDs on graph links; give agents fixed parameterized read-only queries. Compiled layers only for multi-source questions. Build a benchmark from your own questions and let it pick components (CERN chATLAS, 30k+ docs: fine-tuned embeddings + contextual retrieval more than doubled top-1 on the hardest source). Product labels 50 real questions by type to decide if a graph is worth it. Eval of the day: nugget-based completeness (vital nuggets, α-nDCG).

## Content

## Pipeline pattern of the day: end to end

sources (docs, tickets, chat, code) -> incremental connectors that carry permissions -> parse, and add surrounding context to each chunk -> match names to entity IDs and add version links -> index with keyword, vector and graph search, every graph link keeping a source ID -> permission filter -> route the question: lookups to hybrid search and a reranker, questions spanning several sources to the wiki or graph queries, counting and totals to SQL -> cited answer, or decline -> feedback into the eval set

- **Match names to IDs before retrieval.** Telling which company or person a chunk is about is where vector-only search fails ([EDGAR paper](https://arxiv.org/abs/2610.37728)).
- **Keep source record IDs on every graph link,** and give agents fixed read-only queries ([FalkorDB](https://www.falkordb.com/blog/company-brain-ai-agents-graph/)).
- **Build compiled layers like a wiki or graph only for questions that span sources,** and keep plain search for lookups ([LangChain](https://www.langchain.com/blog/building-agent-memory-openwiki-graphs)).
- **Build a benchmark from your own questions first, and let it pick the components.** CERN's [chATLAS](https://arxiv.org/abs/2610.37697) serves over 30k internal docs. On its hardest source, a fine-tuned embedding model plus contextual retrieval more than doubled how often the right doc came first.
- **Treat routing by question type, safety handling, a chat app integration and an MCP server as part of the product,** not extras. chATLAS ships all four.
- **Who owns it:**
  - *Architects* own the routing table from question type to path, and the entity-ID contract across sources.
  - *Product* labels 50 real questions as lookups, multi-source questions or counting. The mix shows whether a graph is worth building.
  - *Devs* put each path behind one interface, and run the benchmark in CI so it decides any component swap.

## Sources

- [EDGAR paper](https://arxiv.org/abs/2610.37728)
- [chATLAS](https://arxiv.org/abs/2610.37697)
- [FalkorDB](https://www.falkordb.com/blog/company-brain-ai-agents-graph/)
- [LangChain](https://www.langchain.com/blog/building-agent-memory-openwiki-graphs)