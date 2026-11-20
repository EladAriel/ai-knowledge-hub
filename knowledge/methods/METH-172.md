# METH-172: Mind the Gap: a deployed multi-agent system that turns support tickets into documentation fixes

## Summary

A triage agent (TriAgent) finds doc gaps from two signals: resolved support tickets, and places where the code and the docs disagree. It then proposes doc repairs, and a person reviews them before they ship. In 43 days of shadow mode it triaged 499 tickets and found 92 doc gaps. Effort: medium. arXiv 2611.23142, Nov 17.

## Details

Numbers: 81.1% of its checkable assertions were correct (245/302, by majority of 3 LLM judges). On length-matched pairs, judges preferred its reply 70.5% of the time vs 23.2% for the human engineer. After a gap was repaired, its re-answer to the same ticket beat its own earlier answer 71.4% of the time (n=35).

Why it matters and limits: these are the first deployed numbers seen so far for a loop that closes doc gaps from tickets. Limits: one organization; judges are mostly LLMs (plus a blinded human audit); the before/after test is small (n=35). Humans still found things the agent missed, so the two complement each other rather than one replacing the other.

Adopt for: Architects add a "gap" record that links the ticket, the missing or stale doc and the fix PR, kept separate from answer logs. Product runs it alongside people first, and measures how many of its gaps they accept, plus before/after answer preference. Devs re-answer the original ticket after each doc fix and store the pair as a free regression case.

## Sources

- [Mind the Gap (TriAgent)](https://arxiv.org/abs/2611.23142)
