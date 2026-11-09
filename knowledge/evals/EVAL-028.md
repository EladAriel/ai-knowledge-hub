# EVAL-028: RAGLog: find which RAG stage broke, using only logs (reference-free fault localization)

## Summary

A logging proxy records the pipeline's API calls, maps them to stages (rewrite, embed, retrieve, rerank, generate) and says which stage failed; no reference answers, no code changes. F1 0.73 on natural faults vs 0.58 Claude Code and 0.52 Codex; ~5 s and ~$0.005 per analysis.

## Details

Limits stated by the authors: labels come from LLM judges, not humans; each pipeline tested in only one configuration. Adopt for: Architects use one shared stage-level trace schema across all RAG apps; Product uses 'which stage fails most' as weekly priority input; Devs run the proxy in staging and add its fault injector to CI. Code: hiraa221/raglog (Docker quickstart, dashboard, fault injector, tests without an API key; borrow the stage format, fault-type list and labeled dataset Hira221/raglog-faults on Hugging Face; research code, very early, 0 stars, last push Oct 24, Apache-2.0). Also listed in the AI methods digest Nov 4 as a new term (F1 0.73, open code).

## Sources

- [RAGLog (arXiv)](https://arxiv.org/abs/2611.03725)
- [hiraa221/raglog](https://github.com/hiraa221/raglog)
- [RAGLog fault dataset](https://huggingface.co/datasets/Hira221/raglog-faults)
