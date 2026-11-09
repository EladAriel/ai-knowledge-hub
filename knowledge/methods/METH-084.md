# METH-084: Length Is Cheap, Competition Is Not: rival statements, not long context, cause context rot

## Summary

Neutral filler up to 32K tokens cost almost nothing; a single conflicting statement about the same fact multiplied the loss 9 to 110 times. For a Company Brain, two versions of the same policy in context are far worse than a long context.

## Details

Caveat: only small open models (0.5B-3B) were tested; code and data are public (yliusci/length-is-cheap). Adopt for: Architects dedupe before indexing and mark old versions as replaced so each fact has one 'current' flag; Product tracks 'conflicting sources' as its own failure type; Devs: when several retrieved chunks give a different value (rest of this part was cut off in the transcript). Term: rival statement = a same-format statement giving a different value for the same fact.

## Content

**2. [Length Is Cheap, Competition Is Not](https://arxiv.org/abs/2611.04169)**
- **The finding:** long context isn't what hurts. Neutral filler up to 32K tokens cost almost nothing.
- **What does hurt:** a single conflicting statement about the same fact multiplied the loss 9 to 110 times.
- **What it means for a Company Brain:** two versions of the same policy in the context are far worse than a long context.
- **Caveat:** only small open models (0.5B to 3B parameters) were tested. The [code and data](https://github.com/yliusci/length-is-cheap) are public.
- Adopt for:
  - *Architects:* before indexing, remove duplicates and mark old versions as replaced, so each fact has one "current" flag.
  - *Product:* track "conflicting sources" as its own failure type.
  - *Devs:* when several retrieved chunks give a valu...ons, like "net revenue," and link them to tables. A gateway controls which models and tools agents can call.
- **Rebrand watch:** this is a business glossary with agent controls added. Airbyte, Context Labs and Avature launched similar "context layer" products this week.
- Adopt for:
  - *Architects:* name a business owner for each core term before you buy any ontology tool.
  - *Product:* start with the top 20 metrics people argue about.
  - *Devs:* serve approved definitions through a tool the agent calls, not as text in the prompt.

2. **When you transfer context to a subagent, only the latest version of the spec and tickets are transferred.** According to the study, length almost does not affect the results, but a contradictory statement on the same fact (for example, an old spec to a new side) increases the error by 9 to 110 times. This is relevant to the problem of the context of your subagents.
   - **Effort:** Tiny.
   - **Source:** [Length Is Cheap, Competition Is Not](https://arxiv.org/abs/2611.04169). Note that only small open models were tested.

And Claude Code 2.1.318 came out tonight, so it's not worth upgrading before it passes the H-15 pin gate. One of the changes in it: if `~/.claude.json` is broken, headless runs fail instead of silently resetting it.

## Sources

- [Length Is Cheap, Competition Is Not (arXiv)](https://arxiv.org/abs/2611.04169)
- [code and data](https://github.com/yliusci/length-is-cheap)