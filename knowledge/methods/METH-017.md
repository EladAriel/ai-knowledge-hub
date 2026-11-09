# METH-017: Authorization outside the model (Privacy Conductor + AFR)

## Summary

LLMs can't decide who may see a document: deterministic gate on human-written policy, model only sees what the requester may see.

## Details

LLM-written labels got sensitivity tier right on 78-86% but rebuilt the ACL correctly on as few as 23%; relabeling gave 13-124 different access decisions per setup (synthetic clinical corpus). Authorization-First Retrieval: retrieve-then-filter exposed unauthorized context in 86.1% of queries. Rule: copy ACLs from the source and enforce outside the model; never put ACL logic in prompts; add negative tests (user X must not see doc Y); zero leaks as launch gate for regulated use cases.

## Content

### 2. [Privacy Conductor: LLMs cannot decide who may see a document](https://arxiv.org/abs/2610.15804) (arXiv, Oct 11) | Effort: **med**
- **What:** a fixed (deterministic) gate applies a policy written by people, and the model only receives what the requester may already see. When LLMs wrote the labels, they got the sensitivity tier right on 78–86% of docs but rebuilt the ACL (access list) correctly on as few as **23%**. Relabeling the same docs gave 13–124 different access decisions per setup. Limitation: the corpus is synthetic clinical data (2,520 requester-document flows).
- **Supporting evidence:** [Authorization-First Retrieval (ACL Anthology 2026)](https://aclanthology.org/2026.trustnlp-main.15/). "Retrieve then filter" pipelines exposed unauthorized context in **86.1%** of queries. Answers leaked 41.3% (Gemini 2.0 Flash) and 29.5% (GPT-4o-mini) of the time. The test set is small (247 chunks).
- **Why it matters:** never let the LLM infer ACLs or "use judgment" about access. Copy ACLs from the source system and enforce them outside the model.
- **Adopt for:**
  - *Architects:* make "authorization happens before any model sees content" a rule in the reference architecture. Have humans or source systems own policy and labels.
  - *Product:* for regulated use cases (HR, legal, health), set "zero permission leaks" as a launch gate, not just a metric.
  - *Devs:* never put ACL logic in prompts. Add negative tests where user X must not see doc Y.

## Sources

- [Privacy Conductor](https://arxiv.org/abs/2610.15804)
- [Authorization-First Retrieval (ACL Anthology 2026)](https://aclanthology.org/2026.trustnlp-main.15/)