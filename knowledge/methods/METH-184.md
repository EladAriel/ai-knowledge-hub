# METH-184: Vendor demos fool the people scoring them: gate, then score (Adopt the method)

## Summary

A global bank's lab scored 10 agent platforms in 9 areas, and each platform got nearly the same score in every area (α=0.98). The scorers were rating how good the demo looked, not what the platform could do. The fix is "gate, then score": first, simple pass-or-fail checks for reliability over repeated runs and for governance; only platforms that pass get scored on quality and business value. arXiv 2611.24039. Next step: turn your own requirements into a pass-or-fail checklist that runs on your data. For: product and architects.

## Details

Noted on Nov 19. Why it matters: use this whenever you choose or pitch a company-brain platform, instead of judging from a demo.

The same day's pipeline practice (PIPE-034) applies the method to the whole system: no permission leaks, every claim has a source, and the system says "I don't know" when the answer isn't there, before any quality score. Repeated runs on your real documents are part of the gate, which also continues the run-to-run noise theme from METH-173.

## Sources

- [Vendor demos fool the people scoring them](https://arxiv.org/abs/2611.24039)
