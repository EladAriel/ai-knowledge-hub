# EVAL-028: RAGLog: find which RAG stage broke, using only logs (reference-free fault localization)

## Summary

A logging proxy records the pipeline's API calls, maps them to stages (rewrite, embed, retrieve, rerank, generate) and says which stage failed; no reference answers, no code changes. F1 0.73 on natural faults vs 0.58 Claude Code and 0.52 Codex; ~5 s and ~$0.005 per analysis.

## Details

Limits stated by the authors: labels come from LLM judges, not humans; each pipeline tested in only one configuration. Adopt for: Architects use one shared stage-level trace schema across all RAG apps; Product uses 'which stage fails most' as weekly priority input; Devs run the proxy in staging and add its fault injector to CI. Code: hiraa221/raglog (Docker quickstart, dashboard, fault injector, tests without an API key; borrow the stage format, fault-type list and labeled dataset Hira221/raglog-faults on Hugging Face; research code, very early, 0 stars, last push Oct 24, Apache-2.0). Also listed in the AI methods digest Nov 4 as a new term (F1 0.73, open code).

## Content

**1. [RAGLog: find which RAG stage broke, using only logs](https://arxiv.org/abs/2611.03725)**
- **How it works:** a logging proxy records your pipeline's API calls and sorts them into stages (rewrite, embed, retrieve, rerank, generate). It then says which stage failed. It needs no reference answers and no code changes.
- **Results:** on naturally occurring faults it scored F1 0.73. Claude Code scored 0.58 and Codex 0.52 on the same task. Each analysis takes about 5 seconds and costs about $0.005.
- **Limits the authors state:** LLM judges made the labels, not people, and each pipeline was tested in only one setup.
- Adopt for:
  - *Architects:* use one shared trace format with stage names across every RAG app.
  - *Product:* use "which stage fails most" as the weekly priority input.
  - *Devs:* run the proxy in staging and add its fault injector to CI.

**[hiraa221/raglog](https://github.com/hiraa221/raglog)** is the code behind insight 1. It has a Docker quickstart, a dashboard, a fault injector, and tests that run without an API key.
- What to borrow: the stage format, the list of fault types, and the [labeled dataset](https://huggingface.co/datasets/Hira221/raglog-faults).
- Maturity: research code, very early, with 0 stars and a last push on Oct 24. Apache-2.0.
- Best for: Devs and Product.

**New names and terms**
- [RAGLog](https://arxiv.org/abs/2611.03725): Fault finding in RAG stages from logs only, without attribution answers. F1 of 0.73, and the code is open.

## Sources

- [RAGLog (arXiv)](https://arxiv.org/abs/2611.03725)
- [hiraa221/raglog](https://github.com/hiraa221/raglog)
- [RAGLog fault dataset](https://huggingface.co/datasets/Hira221/raglog-faults)