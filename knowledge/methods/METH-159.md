# METH-159: Gemini 4 Hydrogen and Orchestrator in Antigravity: a cheap model executes, a dear one replans mid-run

## Summary

Orchestrator hands work back and forth in the same run: Carbon, the heavy model, explores and plans in a read-only stage; Hydrogen, the fast model, makes edits and runs tests; when Hydrogen gets stuck, the work returns to Carbon to fix the plan. Recommendation: Pilot. Effort: medium.

## Details

The split between planner and executor is old. What's new is that this is not a static router that decides the whole task from the first prompt, but a two-way handoff mid-task, with defined conditions for returning to planning. Evidence: according to Google, on Terminal-Bench 4.1 the results are nearly at Carbon's level, with 24% less quota use and 19% more speed. These are vendor numbers, with no independent reproduction yet. Effectiveness 3/5, hype 3/5. Fit is high for any agent product with long tasks. This is the fifth time this week the pattern of a cheap model executing and a dear model stepping in only when needed has come up: Hightouch (Nov 7), Strands (Nov 10), ReTrace (Nov 11), and Gemini Decisions (Nov 12). Continues on Nov 15 with Antigravity /teamwork (METH-168).

## Sources

- [Gemini 4 Hydrogen in Antigravity](https://antigravity.google/blog/gemini-4-hydrogen-in-google-antigravity/)
