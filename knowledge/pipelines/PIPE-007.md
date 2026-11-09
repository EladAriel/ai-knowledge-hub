# PIPE-007: Pipeline: end-to-end company brain

## Summary

connectors with permissions -> parse with doc metadata -> enrich against reviewed ontology -> index (vector+keyword+graph) -> query-time permissions as user -> tiered retrieval -> line-level citations or decline -> session log -> offline memory cleanup.

## Details

Carry the user's identity end to end (live checks, not copied at index time). Human review step on the ontology. Answer the cheapest trusted way first (governed metric, structured query, agent). Version what the system knows (agent writes to branches; derived memories link to source runs). Measure the whole loop: MMEnterprise-Bench found bigger retrieval budgets found more evidence without reliably raising accuracy.

## Content

## Pipeline pattern of the day: end-to-end

connectors with source permissions -> parse, keeping doc-level metadata on every chunk -> enrich against a reviewed ontology -> index (vector + keyword + graph) -> check permissions at query time as the user -> tiered retrieval (governed answer, then structured query, then agent fallback) -> answer with line-level citations, or decline -> session log -> offline memory cleanup, with every lesson linked to its source

- **Carry the user's identity all the way through.** The agent should query as the user, with permissions checked live against the source the way PipesHub does it, not copied once when the index is built.
- **Put a human review step on the ontology.** The LLM proposes changes, and a data steward publishes them, as in the AWS accelerator.
- **Answer the cheapest trusted way first:** a governed metric, then a structured query, then free-form agent search. This is the AWS accelerator's tiered answering.
- **Version what the system knows.** Agent writes go to branches and get merged after review (OmniGraph), and derived memories link back to the runs they came from (the error-reproduction paper).
- **Measure the whole loop, not just retrieval.** [MMEnterprise-Bench](https://mlvlab.github.io/MMEnterprise-Bench/) found that a bigger retrieval budget found more of the evidence but didn't reliably raise answer accuracy.
- **Who owns it:**
  - *Architects* own how identity flows through, the review step for the ontology, and the data contract (chunk metadata, plus memory authority and scope).
  - *Product* owns which tier each use case may use, and what the "I don't know" experience looks like.
  - *Devs* own one local docker-compose setup (PipesHub or OmniGraph), plus a CI job that runs the eval below on every change.

## Sources

- [MMEnterprise-Bench](https://mlvlab.github.io/MMEnterprise-Bench/)