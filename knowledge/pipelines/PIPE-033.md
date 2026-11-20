# PIPE-033: Pipeline: feedback and monitoring — the gap-mining loop (cluster real failures, route to owners, re-answer, close)

## Summary

Today's feedback-and-monitoring angle: turn implicit and explicit production signals into content and connector gaps, route them to owners, re-answer the original question, and promote the case to the golden set. This differs from earlier angles on this stage: regression suite (PIPE around Oct 20), groundedness monitor (Oct 29), and memory-scope audit (Nov 7). See also PIPE-025 for the earlier trace → score → route fix flow.

## Details

Flow: trace everything by default → capture signals (thumbs-down, abstain/"couldn't answer", escalation, user correction, zero-hit search) → cluster weekly → label gap type → route to owner → fix (doc / connector / ACL / retriever) → re-answer the original question → promote the case to the golden set → track gap rate and time-to-close.

Enterprise practices (Nov 18):
- Tracing on by default; production failures become offline tests. In a vendor write-up of Uber, one automatic check found an agent contradicting its own tool results in about 30% of cases, and teams scoring over 90 on evals still had failures that only reading traces exposed ([Arize](https://arize.com/blog/how-uber-evaluates-ai-agents-at-production-scale/)).
- Sort gaps by cause before fixing. Intercom compares failed bot answers with good human replies and flags content as missing, unclear, duplicated or contradictory; nothing is published without a person's OK.
- Track help-center coverage and freshness weekly (Zendesk admin copilot).
- Read each signal differently (HelpCenterKit): a search with no results often means the article exists but uses other words; an unanswered question usually means no article exists; a downvote usually means the article is wrong or out of date.
- Check each fix by re-answering the original question (Mind the Gap, METH-172): after a gap was repaired, the new answer beat the old one 71.4% of the time (n=35).

Who owns it: Architects define one gap_event schema (query, signal type, retrieved sources and scores, user/ACL scope, trace id) and keep ACL context so permission gaps aren't filed as missing content. Product owns the weekly triage, the taxonomy, and owner routing, and reports gap rate and median time-to-close. Devs emit the signals as trace events, build the clustering job, and wire re-answer-after-fix into CI.

## Sources

- [Arize: How Uber evaluates agents](https://arize.com/blog/how-uber-evaluates-ai-agents-at-production-scale/)
- [Intercom Fin content-gap suggestions](https://intercom.help/fin4all/en/articles/11420114-use-ai-powered-content-suggestions-to-improve-fin)
- [Zendesk admin copilot insights](https://support.zendesk.com/hc/en-us/articles/10799529609498-Optimizing-knowledge-with-admin-copilot-insights-and-recommendations)
- [HelpCenterKit: find content gaps](https://helpcenterkit.com/use-cases/find-content-gaps)
- [Mind the Gap (re-answer after fix)](https://arxiv.org/abs/2611.23142)
