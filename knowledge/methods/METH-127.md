# METH-127: WikiTrace and FGSE: memory you can check, and memory approved only after a falsification attempt

## Summary

WikiTrace links every memory lesson to a short note and the original run, so the agent checks the evidence when a lesson is vague, conflicts, or came from a failure. FGSE treats every lesson as a hypothesis: it is tried in a temporary environment against falsification and regression tests, and only then approved, refined, or rejected.

## Details

Both papers attack the same problem: memory-induced degradation (the agent fails a task it could do without memory). This continues the admission/gating line, not a wholly new idea. Retrieval brief (Nov 11): WikiTrace is 10.7 points better than no memory, and 3.2 better than the same lessons without links; it also breaks fewer tasks the agent could already do. Fifth day of the 'every summary should point back to its source' theme. Code maturity: brand new, 2 stars (another review said 3), Apache-2.0. Effort low to medium. Adopt for: Architects—never store a summary without a link to its source; Product—track tasks that got worse because of memory as their own metric; Devs—add source_trace_id and outcome fields to memory records, and give the agent a tool to read them. AI methods digest: WikiTrace was tested on 5 benchmarks, code is open (new repo); FGSE reports 39.8 on WebArena and 78.8 on AppWorld, and 3.6% harmful updates that were approved; neither paper has been independently reproduced. Scores: effectiveness 4/5, hype 2/5. Fit: high for any agent with lasting memory. Effort medium. Recommendation: Pilot. arXiv 2611.14320 (code yukyeongleee/wikitrace) and 2611.14326.

## Sources

- [WikiTrace (arXiv)](https://arxiv.org/abs/2611.14320)
- [wikitrace code](https://github.com/yukyeongleee/wikitrace)
- [FGSE (arXiv)](https://arxiv.org/abs/2611.14326)
