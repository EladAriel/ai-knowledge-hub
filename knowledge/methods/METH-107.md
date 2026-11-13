# METH-107: MEMOIR: credit memories after use, check before compressing

## Summary

Long-horizon agent memory lifecycle without training. Cheap write (no LLM). After each query, retrospective attribution (TRACE) updates importance with a UCB-style exploration bonus; before compression, merges pass judges that check evidence wasn't lost.

## Details

What's new: not static importance at write time (Generative Agents/Mem0) but 'attribute after use, confirm before compress'—close to RMM without training a reranker. Evidence on LoCoMo 1,905 pairs: +11.92 evidence recall@5 vs cosine; verified feedback +1.50; 0/100 merge losses in audit (upper bound 2.95%); write 6.8ms without LLM. Limits: only 10 LoCoMo stores; SUPERSEDE not yet at full scale. Scores: effectiveness 4/5, hype 2/5. Fit: high for agent memory. Effort: medium. Recommendation: Pilot. Also covered in Company Brain Nov 7 brief (same paper).

## Sources

- [MEMOIR (arXiv)](https://arxiv.org/abs/2611.07631)
- [MEMOIR code](https://github.com/AnandMayank/MEMOIR)
