# METH-061: Governed RAG: answer/clarify/decline gate + numeric verifier

## Summary

Production system over 1,143 government procedures: 89.47% of traffic served from fixed templates (~0.67 s); code check confirms every fee/number is in the record.

## Content

**2. [Governed Sovereign RAG for a state government portal](https://arxiv.org/abs/2610.36561)**
- **The setup:** a production system covering 1,143 government procedures. A gate decides whether to answer, ask a clarifying question, or decline to answer.
- **The results:**
  - 89.47% of traffic is answered from fixed templates with no free generation, in about 0.67 s typically.
  - A code check after generation confirms every fee or number appears in the official record. It found 0 invented fees in 40 cases, though that's a small sample.
- **Honest lim...nts completed 38.7% of tasks, versus 10.3% with chunk-based retrieval.
  - Giving the agent the valid code lists stopped it from inventing codes. Invalid payload fields still showed up in 46% of write runs.
  - Giving it full typed context cut invalid calls to 3%.
- **Limitation:** the authors say it doesn't help on OpenAPI services that have no process layer.
- Adopt for:
  - *Architects:* treat process models as part of the ontology, not as separate docs.
  - *Product:* start with one multi-step workflow, like "create order, then approve."
  - *Devs:* always send the schema and the list of valid values along with each tool description.

## Sources

- [Governed Sovereign RAG](https://arxiv.org/abs/2610.36561)
