# METH-023: Agentic RAG via portable skills (Airbnb)

## Summary

SKILL.md + four scripts + one hybrid search tool over an LLM-written wiki: 99.2% procedure match; evidence sufficiency 83.3% vs 59.8% for production RAG.

## Content

**1. [Frustratingly Easy Agentic RAG via Portable Skills (Airbnb)](https://arxiv.org/abs/2610.14428)**
- **What:** a "skill" here is a SKILL.md manual, four scripts, and one hybrid search tool, packaged together. It searches a wiki of about 2,700 pages that an LLM wrote on top of 2,881 support articles. Building it took 1–2 engineer days.
- **Results:** on 132 real cases, 99.2% of answers matched the human-approved procedure. On "evidence sufficiency" (could you rebuild the procedure from the quotes alone?) it scored 83.3%, versus 59.8% for their production RAG service. The two didn't get the same query budget, though.
- **What does the work:** two things carry most of the weight. A code validator rejects any quote that isn't an exact substring of the article it cites. And the wiki merges procedures that are split across articles into one page. Swapping the search algorithm barely mattered; how the content was organized mattered more.
- **Honest limits:** about 90 s per case versus 8–9 s for the production assistant, a mature corpus, and a human reviewing every case. The authors themselves say the wiki is a summary-index pattern similar to RAPTOR, an older summarize-then-search method, not a new mechanism.
- Adopt for:
  - *Architects:* treat the agent's output contract (schema plus exact-quote citations) as a boundary enforced in code, not in the prompt.
  - *Product:* use the gap between "right answer" and "provable answer" to decide where to invest. In Airbnb's case the gap came from missing content, so the fix wa... you can promise and test.
  - *Devs:* add a `supported_by: [[doc_ids]]` field to the extraction output schema from day one.

## Sources

- [Frustratingly Easy Agentic RAG via Portable Skills (Airbnb)](https://arxiv.org/abs/2610.14428)
