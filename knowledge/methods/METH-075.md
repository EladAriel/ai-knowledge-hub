# METH-075: RAGFlow 'Context as Infrastructure': LLM-built structures don't raise accuracy; claim–evidence leaves cut cost

## Summary

A plain keyword-search loop already answered 85% of BrowseComp-Plus and 91% of FRAMES; claims, entity graphs, ontologies, wikis and timelines built at ingest gave no measurable accuracy gain (PageIndex-style outline got worse at scale). The payoff is cost, governance and onboarding.

## Details

What pays off: 'claim–evidence leaves' (small fact + word-for-word quote as proof). When claims alone sufficed, query tokens -91%; otherwise +1.9%; ~38% saving on average. Catch: latency ~3x; a step deciding when to use claims cut it 140 s -> 30 s. Limits: one benchmark, one model building structures, no confidence intervals; FRAMES is English Wikipedia, so company docs (tables, scans, jargon) may do worse. Adopt for: Architects: give each enrichment artifact its own goal (cost, governance, onboarding). Product: track tokens per answer and latency next to accuracy before funding more graph/ontology work.

## Sources

- [RAGFlow: Context as Infrastructure](https://arxiv.org/abs/2610.41172)
