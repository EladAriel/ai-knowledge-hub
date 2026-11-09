# METH-018: Usefulness score + threshold instead of embedding top-k (GPT Researcher)

## Summary

Keep a chunk only if a usefulness score clears a threshold; 73% of kept passages relevant vs 46% with embeddings.

## Details

Jev usefulness score, keep chunks >= JEV_MIN_SCORE=1.5; reports won 15-3 at similar cost (~$0.115). BM25 fallback also beat embeddings (51%). ….

## Sources

- [GPT Researcher context …](https://docs.gptr.dev/docs/gpt-researcher/gptr/context-filter)
