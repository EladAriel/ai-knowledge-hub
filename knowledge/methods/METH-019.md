# METH-019: Always rerank; agentic search only once tuned (Kapa Company Knowledge Bench)

## Summary

7 retrievers on 1,000 production queries: hybrid 0.41, top-100 reranked to 15 = 0.50 for ~0.3 s and no extra tokens.

## Content

**1. [Kapa's Company Knowledge Bench](https://www.kapa.ai/blog/company-knowledge-bench)** (Oct 2)
- Kapa tested 7 retrievers on 1,000 real production queries over docs, Slack, tickets and code. Plain hybrid search scored 0.41. Pulling the top 100 and reranking down to 15 raised that to 0.50, for about a third of a second more and no extra tokens. Splitting the query into sub-queries scored 0.56 but took 1.8 s.
- A frontier model with only grep scored 0.61, the same as a tuned pipeline. But it took 13 to 17 s, cost about $0.17 per query, and returned about 40k tokens, of which only about 1 chunk in 25 was needed. Kapa's own agentic retriever scored 0.65 in about 5 s and returned about 5k tokens.
- Their scoring rules are worth copying. "Complete" means the agent needs nothing else to answer. "Minimal" means no extra chunks. "Source preference" means the authoritative, current page beats a forum post that repeats the same fact. Each test case stores its valid chunks as an AND/OR rule.
- Caveat: this is a vendor benchmark, the data is private, and Kapa built all 7 retrievers. Treat it as a direction, not proof.
- Adopt for:
  - *Architects:* write "minimal set from preferred sources" into the retrieval contract, and add authority and freshness fields to chunk metadata.
  - *Product:* set a latency budget per use case before anyone picks agentic search. A 15 s answer may be fine for research but not for support.
  - *Devs:* add the top-100-then-rerank-to-15 step first, then track tokens returned per query next to accuracy.

...license first.
- Adopt for:
  - *Architects:* put the reranker behind one interface as a swappable service, so a hosted API and a self-hosted model can trade places.
  - *Product:* if data residency is a selling point, this gives you a real self-hosted option.
  - *Devs:* compare it with your current reranker using yesterday's golden set and recall@k.

## Sources

- [Kapa Company Knowledge Bench](https://www.kapa.ai/blog/company-knowledge-bench)
