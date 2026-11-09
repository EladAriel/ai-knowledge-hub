# METH-026: Netflix: ontology-driven observability knowledge graph

## Summary

Telemetry, alerts, deploys, incidents and incident Slack joined into one RDF/OWL graph validated with SHACL; LLM may only output typed facts.

## Details

Every app must match a ~49,000-entry catalog; resolved incidents become knowledge and repeated patterns become detection rules; version the ontology like code. Devs: each enrichment step fetches, analyzes, outputs typed facts only; a slow source degrades rather than blocks. Start with one painful cross-tool question.

## Content

### [Netflix: ontology-driven observability with an incident "knowledge flywheel"](https://netflixtechblog.com/ontology-driven-observability-building-an-end-to-end-knowledge-graph-at-netflix-scale-421392cf5adf)
- **What:** Posted 16 Oct (19:01 Israel time). It joins telemetry, alerts, deploys, incidents and incident Slack into one RDF/OWL graph, validated with SHACL (schema rules). Every application must match a catalog of about 49,000 entries. LLM output must fit typed triples: "it cannot emit a triple that violates the type system."
- **Why it matters:** Resolved incidents become typed knowledge, and repeated patterns become detection rules. Correlation chains below 0.6 confidence are dropped. Agents share one vocabulary, and humans stay as approvers. The post reports no before/after accuracy numbers, only that the "hour or two" of context-gathering now arrives with the alert.
- **Effort:** high
- **Adopt for:**
  - **Architects:** Pick one authoritative catalog per entity type. Version the ontology like code, with changes as pull requests.
  - **Product:** Start with one painful question that spans several tools ("which incidents hit apps owned by team X?").
  - **Devs:** Copy the "enricher contract": fetch, analyze, then emit typed triples only. A slow source should degrade the result, never block it.

## Sources

- [Netflix tech blog](https://netflixtechblog.com/ontology-driven-observability-building-an-end-to-end-knowledge-graph-at-netflix-scale-421392cf5adf)