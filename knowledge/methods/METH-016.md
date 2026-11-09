# METH-016: Agent memory as a Git repo of Markdown (Cognition Agent Memory Repo)

## Summary

Devin memory = git repo of notes; MEMORY.md index per session, source-tagged lines, safe parallel merges, daily 'Dreaming' cleanup.

## Content

### 1. [Cognition open-sourced "Agent Memory Repo": agent memory as a Git repo of Markdown](https://devin.ai/blog/memory-and-dreaming) (Oct 5) | Effort: **low**
- **What:** Devin's memory is now a Git repo of notes. A short `MEMORY.md` (the index) loads into every session. Each note line is one bullet with `[source: <session URL>; added: YYYY-MM-DD]` and `[[path]]` links. Parallel sessions commit and merge, and a stale write gets rejected and retried. A daily "Dreaming" job merges duplicates, drops stale lines, and resolves contradictions ([docs](https://docs.devin.ai/product-guides/memory), [spec, MIT, ~800 stars](https://github.com/AgentMemoryRepo/agentmemoryrepo)).
- **Why it matters:** memory you can read, diff, and audit, where every fact traces back to its source. In the docs, memory is personal and per-org, not shared with the team, so it is not yet a company brain.
- **Slop check:** this is mostly a rebrand of CLAUDE.md-style memory files. The new parts are the provenance metadata, safe concurrent writes, and the scheduled cleanup job. No accuracy numbers were published.
- **Adopt for:**
  - *Architects:* use the line format as a data contract for "learned facts". Decide who owns which folders (team or domain), and that a shared, permissioned memory repo sits separate from personal ones.
  - *Product:* start with one workflow ("agent remembers team conventions"). Track how often users correct the agent, and whether the same correction comes back after a fix.
  - *Devs:* install the skill from the spec repo into Claude Code or Devin. Lint memory files in CI so every line needs `source` and `added`.

## Sources

- [Cognition open-sourced "Agent Memory Repo": agent memory as a Git repo of Markdown](https://devin.ai/blog/memory-and-dreaming)
- [spec repo (MIT)](https://github.com/AgentMemoryRepo/agentmemoryrepo)
- [docs](https://docs.devin.ai/product-guides/memory)
