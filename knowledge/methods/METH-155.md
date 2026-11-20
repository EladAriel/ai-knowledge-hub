# METH-155: Cited but Unused: citations look fine even when the answer came from the model's memory

## Summary

Change a fact in the retrieved passages to a false value and ask again. If the model still gives the original value, it answered from memory, not the context. 1.2–15.7% of claims came from memory, and bigger models did this more; 89–100% of those memory-based claims still had a citation. Also covered in a Nov 13 methods review. Effort: low for an offline check; high if you want an online detector.

## Details

The usual check, testing whether the cited passage supports the claim, did no better than chance at catching this (AUROC about 0.5), even when restricted to the cited passage. The model picks a citation that agrees with what it already wrote. The best detector (token-level with/without-context contrast, AUROC about 0.79) is still too imprecise for production (precision peaks at 0.45). Limits: it only tested small open models (Qwen2.5 0.5B–14B and Llama-3.1-8B, on ASQA), and only on number and date claims; a title-leak artefact that the authors corrected roughly halved their earlier rates; the paper's code link was broken (404) when the brief was written. Rebrand check: this builds on known work about models choosing citations after the fact (Wallat et al. 2025) and the Nov 4 counterfactual-swap eval. What's new is the base rate, and that NLI checking can't see this failure. Adopt for: Architects treat "has a citation" and "passes NLI" as support signals, not provenance, and take high-stakes values (prices, dates, limits) from a system-of-record lookup; Product should not market "every answer is cited" as a guarantee of grounding; Devs add an offline value-swap job on 50 numeric golden questions and track the memory-based claim rate per model upgrade. arXiv 2611.17161.

## Sources

- [Cited but Unused](https://arxiv.org/abs/2611.17161)
