# METH-077: DeepSeek dsh-superagent-prototype: Fixed router over isolated workers

## Summary

A code agent that works continuously on one repo: Router receives events from GitHub/Feishu and distributes 'tickets' to Workers, each in their own session and folder until PR.

## Content

**1. [DeepSeek dsh-superagent-prototype](https://github.com/deepseek-ai/dsh-superagent-prototype)**
- **What it is:** A code agent that continuously works on one repo. A permanent router receives events from GitHub or Feishu and distributes "tickets" to isolated workers. Each Worker works in its own session and folder until a PR is opened.
- **Why new:** The division into Router and Workers is a partial rebrand of orchestrator-worker. What's really new:
  - The session is not exposed to the user. A Worker subscribes to a thread and receives events from it directly.
  - Proactive work is only allowed according to rules written by the team in advance.
  - Speculative execution: the agent recovers and fixes a bug in the background, and only reports if it has found a fix.
  - Everything is formulated around saving human attention.
- **Evidence:**
  - The open source (MIT), together with the prompts and the architecture documents.
  - DeepSeek defines it as a research prototype and not as a product, and says that part of the design in the article has not yet been realized.
  - The speed data that rotates in X comes from their simulations and has not been verified.
- **Scores:** Effectiveness 4/5, Hype 3/5.
- **Fit:** High for any organizational assistant that works all the time (Slack, tickets, email). **medium** effort.
- **Recommendation: Pilot** for the pattern itself, not for the code. Yesterday it appeared only in the list of terms.

## Sources

- [dsh-superagent-prototype](https://github.com/deepseek-ai/dsh-superagent-prototype)
