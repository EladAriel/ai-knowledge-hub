# METH-180: Multi-agent memory that keeps contradictions instead of resolving them (Pilot)

## Summary

Two papers. The first shows that when workers pass findings to a lead, contradictions disappear along the way: workers retrieve both conflicting claims in 68.7% of cases, but report both only 35.2% of the time. The second tested five memory mechanisms, and only one passed: give the agents the ranked list of contradictions instead of a "winning fact". F1 rose by 0.34, and successful poisoning attacks fell from 22 to 7 of 122, at the same cost. Recommendation: Pilot. Effort: medium. arXiv 2611.22245 and 2611.22461.

## Details

What is new: the papers measure exactly where contradictions are lost. The idea itself is close to DISCERN (METH-145, Nov 13–14), which keeps everything at write time and decides at read time, so this is a strengthening, not a new idea.

Evidence: numbers with confidence intervals and statistical tests, and in the second paper the thresholds were set in advance. This is controlled research, not production. Effectiveness 3/5, hype 1/5. Fit is high for enterprise knowledge systems and multi-agent RAG. Effort is medium: add a contradictions field to the report the worker sends the lead. The memory theme has been constant: DISCERN on Nov 14 and MemCredit on Nov 15 (METH-169). Nov 19 update: on Harvey LAB legal-document tasks, splitting work raises collection of both conflicting claims from 50% to 69%, but the lead's conflict detection falls from 16% to 13%, because workers report both claims only 35% of the time. Recommendation updated to an Adopt-check (low effort): require subagents to pass conflicting evidence explicitly. A concrete way to do it: add a required `conflicts` field to the subagent report.

## Sources

- [Contradiction loss in worker-to-lead reports](https://arxiv.org/abs/2611.22245)
- [Memory that keeps a ranked contradiction list](https://arxiv.org/abs/2611.22461)
