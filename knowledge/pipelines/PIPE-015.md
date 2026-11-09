# PIPE-015: Pipeline: feedback & monitoring v2 (log what the model saw) + unsupported-claim monitor

## Summary

record full trace incl. final context -> cheap live judges/rules -> route feedback by failure type -> find failed stage ….

## Details

Log what the model actually saw (cut tool output, dropped fields). Route thumbs-down into owned queues (missing knowledge, parsing, chunking, wrong version, retrieval, generation, permissions, UX). ….

## Sources

- [monitor decision value](https://arxiv.org/abs/2610.36544)
- [Annotrace](https://arxiv.org/abs/2610.23284)
- [Confident AI guide](https://www.confident-ai.com/knowledge-base/guides/rag-evaluation)
