# METH-109: Calibrated decision model as filter, strong model for the gray zone (Hightouch + Kev)

## Summary

At Hightouch, Jev checks identity-profile matches; only 30%–90% confidence cases go to Opus. Related paper: Kev-4B filters retrieved passages against injections and spoofed pages (Decision Models as Retrieval Gates).

## Details

What's interesting: calibration matters—Luna alone is more accurate, but overconfidence hurts it in the cascade. Hightouch reports 98.8%/95.3% vs Opus-alone 99.0%/95.1% at 4.4×/1.8× lower cost (internal 1,000 synthetic identities, no code). Filter paper: attack success 13.6%→5.7%, 4 false alarms / 186 clean pages, 76 ms/passage. Effectiveness 4/5 · hype 2/5. Fit: high for RAG filters, eval, guardrails. Effort: medium. Recommendation: Pilot. Continues Jev/JevAct line.

## Sources

- [Hightouch LLM judges](https://hightouch.com/blog/llm-judges-identity-resolution)
- [Decision Models as Retrieval Gates](https://arxiv.org/abs/2611.08325)
