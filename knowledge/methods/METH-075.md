# METH-075: RAGFlow 'Context as Infrastructure': LLM-built structures don't raise accuracy; claim–evidence leaves cut cost

## Summary

A plain keyword-search loop already answered 85% of BrowseComp-Plus and 91% of FRAMES; claims, entity graphs, ontologies, wikis and timelines built at ingest gave no measurable accuracy gain (PageIndex-style outline got worse at scale). The payoff is cost, governance and onboarding.

## Details

What pays off: 'claim–evidence leaves' (small fact + word-for-word quote as proof). When claims alone sufficed, query tokens -91%; otherwise +1.9%; ~38% saving on average. Catch: latency ~3x; a step deciding when to use claims cut it 140 s -> 30 s. Limits: one benchmark, one model building structures, no confidence intervals; FRAMES is English Wikipedia, so company docs (tables, scans, jargon) may do worse. Adopt for: Architects: give each enrichment artifact its own goal (cost, governance, onboarding). Product: track tokens per answer and latency next to accuracy before funding more graph/ontology work. Devs: prototype claim–evidence pairs (fact, quote, source ID) on one corpus and measure the sufficiency rate (share of questions the claims alone answer).

## Content

**1. [RAGFlow: "Context as Infrastructure"](https://arxiv.org/abs/2610.41172)**
- **The finding:** a plain keyword-search loop already answered 85% of BrowseComp-Plus and 91% of FRAMES. Extra structures built by LLMs at ingest time didn't help:
  - Claims, entity graphs, ontologies, wikis and timelines gave no measurable accuracy gain.
  - A PageIndex-style outline got worse at scale.
- **What does pay off:** "claim–evidence leaves," meaning small facts stored with a word-for-word quote as proof.
  - When the claims alone were enough to answer, they cut query tokens by 91%. When they weren't, tokens rose only 1.9%, for a 38% saving on average.
  - The catch is latency, which roughly tripled. A step that decides when to use the claims brought it from 140 s down to 30 s.
- **Limits they state:** one benchmark, one model building the structures, and no confidence intervals. FRAMES is English Wikipedia, so company docs with tables, scans and jargon may do worse.
- Adopt for:
  - *Architects:* give each enrichment artifact its own goal (cost, governance or onboarding), instead of expecting it to boost accuracy.
  - *Product:* track tokens per answer and latency next to accuracy before funding more graph or ontology work.
  - *Devs:* prototype claim–evidence pairs (fact, quote, source ID) on one corpus, and measure how often the claims alone are enough.

**2. [Context as Infrastructure: Knowledge Compilation (RAGFlow)](https://arxiv.org/abs/2610.41172)**
- **What it is:** When the agent search harness is good, most of the accuracy problem is solved, and the bottleneck goes to the context. Their solution is a "compilation" phase during ingestion. It builds a navigation tree whose leaves are a claim with its evidence, alongside an ontology, a graph, a wiki and a timeline.
- **Why new:** This is partially a rebrand of enrichment while indexing, in the style of GraphRAG or PageIndex. What is new is the framing of the "context delivery layer, not a better retriever", and the honest measurement.
- **Evidence:**
  - BM25 or grep with harness reached 85% in BrowseComp-Plus and 91% in FRAMES, without vector index.
  - The tree saves 91% of the toucans when the evidence is sufficient, and 38% on average.
  - Decision gate lowered the latency from 140 seconds to 30.
  - They admit that the additional structures were not used by agents again, after 21.10, when agents weakened monitors, and 27.10, when the CoT hid an operation.

## Sources

- [RAGFlow: Context as Infrastructure](https://arxiv.org/abs/2610.41172)