# METH-095: When Do Summaries Become Instructions?: fabricated policy in handoff/compaction summaries

## Summary

Measures whether long-horizon agent compaction summaries invent permissions or limits that are not in the record, and whether the inheriting agent acts on them. Checked against a real permission ledger with replay from the same snapshot. First time compaction is measured as a source of forged policy, not only of information loss.

## Content

**2. [When Do Summaries Become Instructions? Fake policy in handoff summaries](https://arxiv.org/abs/2611.06545)** ([code](https://github.com/Chuw1/handoff-audit))
- **What is this:** Checking whether the compaction summaries of a long-term agent invent permissions or limitations that do not exist in the record, and whether the successor agent acts according to them. The test is done against a real permission book, with a repeat run from the same snapshot.
- **Why new:** For the first time someone measures the compaction as a source of fake policy, and not only as a source of information loss.
- **Evidence:**
  - Unsubstantiated endorsements appeared in 0.1% to 1.3% of summaries.
  - Neutralizing them dropped unauthorized actions from 24 to 7 out of 120 runs, but that's a post-hoc finding. In the later set the drop was only from 17 to 11 out of 48.
  - A strong and premeditated finding: rewording the system prompt line "Some actions need approval" lowered invented limits from 1.8% to 0.3% (p < 10⁻⁹).
  - The effect on self-limitations is fragile, and the author reports this openly.
- **Scores:** Effectiveness 3/5, Hype 1/5.
- **Compatibility:** For any agent with compaction or handoff; Add an eval that compares the summary to the permission book. **low** effort.
- **Recommendation: Adopt** as eval and as a wording correction. The subject of compaction returns after SJC on 16.10 and the agent_summary calls on 29.10.

From today's digests, one item passed the filter, and is in the queue for 9:00 Sunday in queue H-17:
- **Source:** [When Do Summaries Become Instructions?](https://arxiv.org/abs/2611.06545) ([Code](https://github.com/Chuw1/handoff-audit))

And an update to yesterday's warning: According to the DevEx Radar, Postman says it is eliminating the automatic installation of plugins. What's already installed doesn't go away by itself, so it's still worth checking, and H-16 is still relevant.

## Sources

- [When Do Summaries Become Instructions? (arXiv)](https://arxiv.org/abs/2611.06545)
- [handoff-audit](https://github.com/Chuw1/handoff-audit)
