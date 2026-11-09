# METH-064: Compiled wiki + evidence graph for multi-source questions (LangChain, FalkorDB)

## Summary

Compiled wiki raised multi-doc accuracy 0.10 -> 0.52 (cost per correct $0.55 -> $0.19); no gain on simple lookups.

## Details

LangChain: 111 synthetic insurance docs, 972-fact key; evidence graph (claims linked to passages) +27% accuracy, 2x citation consistency, -58% cost per correct; lookups 0.84 vs 0.83 and slower; wiki compile $4.15 + ~$0.09/doc; ….

## Sources

- [LangChain OpenWiki + graphs](https://www.langchain.com/blog/building-agent-memory-openwiki-graphs)
- [FalkorDB company brain](https://www.falkordb.com/blog/company-brain-ai-agents-graph/)
- [inherit-brain](https://github.com/zeyusuntt/inherit-brain)
