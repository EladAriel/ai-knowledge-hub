# METH-064: Compiled wiki + evidence graph for multi-source questions (LangChain, FalkorDB)

## Summary

Compiled wiki raised multi-doc accuracy 0.10 -> 0.52 (cost per correct $0.55 -> $0.19); no gain on simple lookups. Graph company brain scored 80.0 vs 19.2 hybrid RAG.

## Details

LangChain: 111 synthetic insurance docs, 972-fact key; evidence graph (claims linked to passages) +27% accuracy, 2x citation consistency, -58% cost per correct; lookups 0.84 vs 0.83 and slower; wiki compile $4.15 + ~$0.09/doc; claim-hash check flags stale claims without a model call. FalkorDB hackathon winner inherit-brain: Salesforce HERB in 30 graphs, 1,203 held-out questions, 80.0 vs 39.2 retrieval tools vs 19.2 hybrid RAG, ~1/5 the tokens. Route only multi-source questions to the wiki/graph.

## Content

**1. [LangChain: agent memory with OpenWiki and an evidence graph](https://www.langchain.com/blog/building-agent-memory-openwiki-graphs)** (Oct 28)
- **The test:** 111 synthetic insurance docs that amend and override each other, checked against an answer key of 972 facts.
- **Results:**
  - On questions that connect several docs, an agent with a compiled wiki went from 0.10 to 0.52 accuracy. Cost per correct answer fell from about $0.55 to $0.19.
  - On 80 simple lookups it made no difference (0.84 vs 0.83) and was slower (12s vs 9s).
  - Adding an "evidence graph," where each wiki claim links to the passage behind it, raised accuracy 27% and doubled citation consistency. It also cut cost per correct answer by 58%.
- **Limits:** the docs are synthetic and LangChain ran the test itself. Compiling the wiki cost $4.15, plus about $0.09 per new doc.
- Adopt for:
  - *Architects:* treat the wiki as a layer you can rebuild from sources, with every claim linked to its source lines.
  - *Product:* send only questions that span several sources to the wiki, and keep plain search for lookups.
  - *Devs:* copy its claim-hash check, so editing a source flags stale claims without a model call.

**2. [FalkorDB hackathon: a company brain on a graph](https://www.falkordb.com/blog/company-brain-ai-agents-graph/)** (Oct 29)
- **The winner:** [inherit-brain](https://github.com/zeyusuntt/inherit-brain) loaded Salesforce's HERB enterprise dataset into 30 graphs. On 1,203 held-out questions it scored 80.0, against 39.2 for retrieval tools and 19.2 for hybrid RAG. It used the same model and about a fifth of the tokens.
- **How it's ...enwiki](https://github.com/langchain-ai/openwiki)** is a command-line tool and MCP server that compiles repos and docs into a linked Markdown wiki, with each claim linked to its source. It works inside Claude Code, Cursor and Codex.
- What to borrow:
  - Hashes on each claim's sources, to spot stale pages.
  - Search and read tools that make no model calls.
  - Linked workspaces across several repos.
- Maturity: about 17.6k stars and 1.3k forks, last push Oct 29, MIT license. Install with `npm install -g openwiki`.
- Best for: Devs.

## Sources

- [LangChain OpenWiki + graphs](https://www.langchain.com/blog/building-agent-memory-openwiki-graphs)
- [FalkorDB company brain](https://www.falkordb.com/blog/company-brain-ai-agents-graph/)
- [inherit-brain](https://github.com/zeyusuntt/inherit-brain)