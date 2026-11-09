# METH-037: MemoryTax: keep raw history, search it agentically

## Summary

With Opus 5.5, an agent searching raw history scored 99% at under half the cost of full context; Mem0 only beat full context with GPT-4o-mini.

## Details

'Writer ceiling': what the memory step drops at save time can't be recovered later. One conversation, one run per setting. Keep raw sources and treat extracted facts as a rebuildable layer; version the extraction step by model + prompt hash; rerun memory vendors on your own data.

## Content

**4. [MemoryTax: the bitter lesson of agent memory](https://arxiv.org/abs/2610.29823)** (arXiv, Oct 22)
- The authors compared full context, BM25 keyword search, Mem0, Zep, and coding agents that search the raw history. Mem0 only beat full context when paired with GPT-4o-mini. With Opus 5.5, an agent searching the raw history scored 99% at less than half the cost of full context.
- They call one limit the "writer ceiling." Whatever the memory step leaves out when saving can't be recovered later, even by a stronger model reading it.
- Limitation: it's one conversation with one run per setting. It's also an old idea under a new name, echoing yesterday's "keep the raw evidence" paper and [Redis's memory benchmark](https://redis.io/resources/agent-memory-benchmark-report/).
- Adopt for:
  - *Architects:* keep the raw sources, and treat extracted facts as a layer you can rebuild.
  - *Product:* rerun memory vendors on your own data before choosing one.
  - *Devs:* version the extraction step by model and prompt hash.

## Sources

- [MemoryTax](https://arxiv.org/abs/2610.29823)
- [Redis's memory benchmark](https://redis.io/resources/agent-memory-benchmark-report/)