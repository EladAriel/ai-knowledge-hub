# METH-030: Databricks MemCurrent: episodic + derived memory with dreaming

## Summary

Append-only session logs plus distilled lesson files with an auto memory.md index; pass rate 22.3% -> 68.4%, 31% fewer tokens.

## Content

**1. [Databricks MemCurrent: persistent memory for production agents](https://www.databricks.com/blog/memcurrent-designing-persistent-memory-production-agents)** (Oct 20)
- **Two memory types:** episodic memory is the raw session logs, which are only ever added to. Derived memory is distilled lessons stored as files. An auto-generated `memory.md` index of them is loaded at session start, so the agent knows what it knows.
- **Two ways to write memory:** explicit tools (`add/update/delete_memory`) handle "remember this," and an offline "dreaming" job distills lessons and merges duplicates. Dreaming alone scored 63.5%, tools alone 53.9%, and both together 66.1%.
- **Results:** on an internal benchmark built from real Genie sessions (Genie is Databricks' AI assistant), the pass rate rose from 22.3% with no memory to 68.4%. Runs also used 31% fewer tokens and were 26% faster. Mem0 scored 43.9% on the same benchmark. On public benchmarks it matched putting everything in context while using about 12x fewer input tokens. Caveat: the internal benchmark is only 114 cases, and Databricks ran it.
- This is the second time "dreaming" has come up (Cognition's version was in Saturday's brief), so it's becoming a standard pattern.
- Adopt for:
  - *Architects:* split memory into a log that's only appended to plus a curated store that can change, and give the cleanup job a clear owner.
  - *Product:* track "rediscovery cost," meaning tool calls per repeat question, as a success metric.
  - *Devs:* start with a `memory.md` index plus `search_memory` and `fetch_memory` tools before building anything fancier.

## Sources

- [Databricks MemCurrent](https://www.databricks.com/blog/memcurrent-designing-persistent-memory-production-agents)
