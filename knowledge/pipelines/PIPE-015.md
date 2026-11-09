# PIPE-015: Pipeline: feedback & monitoring v2 (log what the model saw) + unsupported-claim monitor

## Summary

record full trace incl. final context -> cheap live judges/rules -> route feedback by failure type -> find failed stage -> fix -> regression set -> CI -> confirm live.

## Details

Log what the model actually saw (cut tool output, dropped fields). Route thumbs-down into owned queues (missing knowledge, parsing, chunking, wrong version, retrieval, generation, permissions, UX). Score retrieval and generation separately; alert per group vs rolling baseline. Staged rollout: shadow, internal, % traffic, kill switch. Judge a monitor by decision value (a 90%-accurate restart monitor ranged -5 to +35 pts). Eval: split answers into claims, cheap judge supported/unsupported/contradicted with escalation, hand-label ~100 traces (Annotrace), chart unsupported-claim rate per group vs last 7 days, log stale co-retrieval.

## Content

## Pipeline pattern of the day: feedback and monitoring

record the full trace (question, retrieved chunks, final context, tool inputs and outputs, answer, citations, user signal) -> score live traffic with cheap judges and rules -> sort feedback by failure type -> find the stage that failed -> fix it -> add the case to the regression set -> gate in CI -> confirm on live traffic

- **Log what the model actually saw,** not just what you retrieved, including cut tool output and dropped fields, as in the "Context Is a Pipeline" paper.
- **Send each thumbs-down to a queue** by failure type: missing knowledge, parsing, chunking, wrong version, retrieval, generation, permissions or UX. Each queue has its own owner ([data engineering handbook, ch. 23](https://datascale-ai.github.io/data_engineering_book/en/part7/ch23_online_feedback_knowledge_update/)).
- **Score retrieval and generation separately.** Alert per group, such as source, question type or pipeline version, against a rolling baseline, because damage is usually local ([Confident AI guide](https://www.confident-ai.com/knowledge-base/guides/rag-evaluation)).
- **Roll out in stages:** first in shadow mode, where the system runs without users seeing its answers, then internal users, then a share of traffic, with a kill switch. Your best signal is a user who opens the cited source and then flags the answer ([Basilin Joe](https://basilinjoe.github.io/blog/rag-in-production)).
- **Judge a monitor by what acting on its alerts achieves, not by its accuracy.** [This study of a monitor that restarts agents](https://arxiv.org/abs/2610.36544) found a 90%-accurate monitor could mean anything from a 5-point loss to a 35-point gain.
- **Who owns it:**
  - *Architects* own the trace format as a data contract, and the list of feedback types.
  - *Product* owns how often feedback gets triaged, the success metrics per group, and the rule that a fix only counts once it's a test.
  - *Devs* own the tracing ...policy and pricing.
2. Split each answer into claims, and ask a cheap judge whether each one is supported, unsupported or contradicted by the context. Send low-confidence cases to a bigger judge.
3. Label about 100 traces by hand once, and check how often the judge agrees with you. A tool like [Annotrace](https://arxiv.org/abs/2610.23284) gives that labeling a structure.
4. Chart the unsupported-claim rate per group against the last 7 days, and alert on jumps.
5. Also log stale co-retrieval, meaning how often an old and a new version of the same doc appear in one context.

**What it catches:** hallucinations after an index rebuild, answers based on outdated policy, cut-off evidence, and quiet changes from a new model or prompt.

**Who runs it:** Devs build it. Product owns the alert thresholds and triage. Architects make sure the trace records the final context.

## Sources

- [monitor decision value](https://arxiv.org/abs/2610.36544)
- [Annotrace](https://arxiv.org/abs/2610.23284)
- [Confident AI guide](https://www.confident-ai.com/knowledge-base/guides/rag-evaluation)
- [data engineering handbook, ch. 23](https://datascale-ai.github.io/data_engineering_book/en/part7/ch23_online_feedback_knowledge_update/)
- [Basilin Joe](https://basilinjoe.github.io/blog/rag-in-production)