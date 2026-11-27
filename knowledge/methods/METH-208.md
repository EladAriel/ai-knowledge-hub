# METH-208: Shared agent memory needs scopes

## Summary

An agent that learns from one user can leak that user's private facts to everyone else. The fix is to label every saved lesson with who can use it: one user and one agent, the user, the agent, or everyone. Why it matters: up to +16 points versus no memory, and at most 0.02% of privacy probes found a leak. That's a benchmark only, with 5 users and 7 agents. For: product and devs. arXiv 2611.10439.

## Details

Reported Nov 24. Complements today's permissions practice in PIPE-039, which also keys agent memory by the user's permission set.

## Sources

- [Shared agent memory needs scopes](https://arxiv.org/abs/2611.10439)
