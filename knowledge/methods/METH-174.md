# METH-174: Living Context Graphs: an enterprise semantic layer learned from verified query outcomes

## Summary

A context layer that sits on top of the warehouse without copying it. It bootstraps semantics from the data, indexes business context as queries are served, and writes durable learnings from verified outcomes. When later outcomes contradict a learning, it withdraws it, and the learning can earn its way back. Effort: high. arXiv 2611.20976, Nov 16.

## Details

Evaluated as text-to-SQL on 3 BIRD databases (353 history questions, 146 held out). Bootstrapping alone adds +4.6 points. Learning from history adds +22.6 points on the untouched held-out set (CI +14.4 to +30.8), which beats 5-shot retrieval from the same history by +12.3. Removing the graph changes accuracy by at most one question per database but raises cost 2.3–3.3× and median latency 1.8–3.4×. So the learned semantics drive accuracy, and the graph drives efficiency.

Limits: BIRD only, 146 held-out questions. The linked repo (varunagrawal2002/Living-Context-Graph) holds only data splits and a README (no code; last commit Sep 7, 2026). Rebrand note, from the brief: this is the semantic layer / metric view idea, now with a feedback loop that writes back.

Adopt for: Architects let only verified outcomes write to the semantic layer, and give each learning a withdraw path. Product reports held-out accuracy separately from in-history accuracy. Devs log (question, SQL, verified?, which learnings were used) so withdrawals can be traced back.

## Sources

- [Living Context Graphs](https://arxiv.org/abs/2611.20976)
- [LCG repo (data splits only)](https://github.com/varunagrawal2002/Living-Context-Graph)
