# METH-111: Anthropic: The components of agent memory (dreaming / sleep-time compute)

## Summary

'Dreaming' is an offline pass where the agent rereads session logs, fixes wrong notes, merges duplicates, and builds a linked wiki (idea credited to Letta and Berkeley sleep-time compute). Search+wiki 61% vs search-alone 53% on ~350k Stainless files / 25 questions, ~20k fewer tokens/question; multi-doc merger questions 87% vs 73%.

## Details

Limits: Anthropic's own evals; wiki didn't help when one doc already held the answer; dreaming costs compute; wiki can grow larger than sources. Lessons: keep session-start memory file small (Claude Code reads first 200 lines / 25 KB of MEMORY.md); explain why memory exists—rigid 'only record failures' erased most gains. Effort: medium. Adopt for: Architects treat wiki as derived layer always checked against raw sources; Product start with multi-doc questions. Methods digest Nov 8: effectiveness 4/5 · hype 2/5; Pilot; internal Stainless ~420M tokens, Harvey LAB merger 87% vs 73%; shared table kept 41/57 facts vs per-contract page with verbatim cite 57/57.

## Sources

- [Anthropic agent memory](https://www.anthropic.com/research/components-of-agent-memory)
- [sleep-time compute](https://arxiv.org/abs/2504.13171)
