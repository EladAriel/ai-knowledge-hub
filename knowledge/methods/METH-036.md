# METH-036: Persistent memory injection across sessions

## Summary

An injected instruction saved to assistant memory fires again in later sessions (shown on ChatGPT, Claude, Gemini); shared org memory spreads it.

## Content

**[arXiv 2610.28810](https://arxiv.org/abs/2610.28810)** (arXiv, Oct 22)
- An injected instruction gets saved to an assistant's persistent memory and fires again in later sessions. The authors showed this on ChatGPT, Claude and Gemini.
- Ways in include skills, org-wide instructions, and resources connected through MCP (the protocol agents use to reach tools and data). Shared org memory let one attacker affect several users.
- Nearly half of the defenses they propose aren't implemented in the services they tested. Their attack code is in [Memory-injection](https://github.com/PedroBarcha/Memory-injection), which has 1 star and no license.
- Adopt for:
  - *Architects:* mark ingested content as untrusted, keep shared memory separate from per-user memory, and require approval for shared writes.
  - *Product:* add "who can write to shared memory?" to rollout reviews.
  - *Devs:* plant injection test strings in your test documents.

## Sources

- [memory injection paper](https://arxiv.org/abs/2610.28810)
- [attack code](https://github.com/PedroBarcha/Memory-injection)
