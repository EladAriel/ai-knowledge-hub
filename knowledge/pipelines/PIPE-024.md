# PIPE-024: Pipeline: the answer layer (structured disposition + code checks)

## Summary

reranked evidence -> drop non-evidence text and cap budget -> structured answer (claims, citations, numbers, decision) -> code checks (schema, citations, numbers) -> answer, clarify, or decline.

## Details

Make disposition an explicit field (answer/clarify/abstain + reason); force structured output with a real schema (OpenAI/Claude structured outputs or instructor); every cited ID must have been retrieved; check numbers/units/periods after generation with code/solver (VeriFin); remove non-evidence context before generating (Intrusion Pathway). Owners: Architects (decision field, check rules); Product (when UI shows clarify/decline); Devs (schema + CI checks; keep policy out of the prompt).

## Sources

- No external source link (in-house technique note).
