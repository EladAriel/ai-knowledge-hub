# TOOL-025: Repos: RAGFlow, Pydantic AI, NeMo Guardrails

## Summary

RAG engine with source-traced citations and depth levels; typed agent framework with agentic evaluators; programmable rails.

## Details

infiniflow/ragflow (~93k, Apache-2.0, 1.0 RC): citation UI, 'thinking mode' depth Low-Ultra for fast vs deep paths. pydantic/pydantic-ai (~21k, MIT): typed outputs, durable execution, OTel, agentic evaluators grading tool-call sequences in CI. NVIDIA-NeMo/Guardrails (~7.4k, Apache-2.0): fact-checking and output-moderation rails for RAG.

## Content

**[RAGFlow](https://github.com/infiniflow/ragflow)** is an open-source RAG engine with multi-step agentic retrieval and citations that trace back to the source.
- What to borrow: its citation UI, and its "thinking mode" depth levels from Low to Ultra, for sending cheap questions down a fast path and hard ones down a deep path.
- Maturity: about 93k stars, Apache-2.0, pushed today, 1.0 release candidate, runs with `docker compose`.
- Best for: Product, to try use cases fast, and Architects, as a reference architecture.

**[Pydantic AI](https://github.com/pydantic/pydantic-ai)** is a typed Python agent framework with guardrails, durable execution and OpenTelemetry tracing.
- What to borrow: its typed outputs, and its [agentic evaluators](https://pydantic.dev/docs/ai/evals/evaluators/agentic/), which grade the sequence of tool calls, for CI.
- Maturity: about 21k stars, MIT, active.
- Best for: Devs.

**[NeMo Guardrails](https://github.com/NVIDIA-NeMo/Guardrails)** is NVIDIA's library of programmable checks ("rails") on inputs, outputs and retrieval.
- What to borrow: the fact-checking and output-moderation rails for RAG answers.
- Maturity: about 7.4k stars, Apache-2.0, release 0.24.1, `pip install nemoguardrails`.
- Best for: Architects, as a central policy layer.

## Sources

- [ragflow](https://github.com/infiniflow/ragflow)
- [pydantic-ai](https://github.com/pydantic/pydantic-ai)
- [NeMo Guardrails](https://github.com/NVIDIA-NeMo/Guardrails)
- [agentic evaluators](https://pydantic.dev/docs/ai/evals/evaluators/agentic/)