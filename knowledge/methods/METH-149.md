# METH-149: How Glean evaluates retrieval for agents

## Summary

Glean measures recall in the top 8 and top 16 results, because its search tool returns 8–16 results and the LLM reads all of them, not just the top 1–3 like a person would. A per-source citation chart caught a Slack logging bug that offline evals missed. Hamel Husain guest talk, Nov 12. Effort: low to copy the metrics, medium to build the setup that replays real queries.

## Details

Other retrieval metrics: how high the right document ranks; how much the result order shuffles between versions; whether the snippets actually cited made it into the context. Answer metrics: two-way judge comparisons for completeness and correctness, plus citation quality, tool failures, tokens, latency and loop count. Real story: a logging bug dropped Slack threads, and the offline evals missed it. Tracking citations per data source caught it, because Slack suddenly stopped getting cited. Adopt for: Architects make "data source" a required field on every retrieval and citation log, so you can break metrics down by source; Product put each source's share of citations on the launch dashboard, and treat a sudden drop as top priority; Devs measure recall at the number of results the agent actually gets, like 16, not 10 out of habit.

## Sources

- [Glean talk (YouTube)](https://www.youtube.com/watch?v=hzWv-apa4k4)
- [Hamel Husain's notes](https://content.delphi.co/hamel/how-to-evaluate-agent-retrieval-810066338bb2)
