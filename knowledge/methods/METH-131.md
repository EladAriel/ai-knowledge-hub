# METH-131: One agent vs multi-agent on 13 company procedures

## Summary

The study kept the model, tasks and tools the same and changed only the agent design. No design won overall.

## Details

Results: multi-agent and skill-based setups used 1.4–4.7 times the tokens and took 2.6–5.8 times as long, usually for small gains that were rarely significant. Well-written skills helped, taking success from 67.4% to 73.1%, while badly written ones hurt. Only a carefully redesigned multi-agent setup clearly beat a single agent, at 75.6%. Effort: low. It's a rule for decisions, not code. Adopt for: Architects—default to a single agent, and require cost per successful task before approving multi-agent; Product—choose the design per workflow, not company-wide; Devs—review skills against a checklist, since skill quality mattered more than the design. arXiv 2611.12953.

## Sources

- [one agent vs multi-agent (arXiv)](https://arxiv.org/abs/2611.12953)
