# METH-128: AlphaProof Code (Google DeepMind): formal verification of Signal's code

## Summary

Human experts and models write the specification together. Then Gemini Carbon-based agents prove in Lean that the compiled code meets the security properties. The blog says more than 6 million lines of Lean were written, and only about 1% were marked for human review.

## Details

What's new: according to DeepMind, this is the first time a widely used protocol's implementation was verified at the code level, not only at the design level. The general pattern: a human approves a spec, an agent does the work, and a deterministic checker verifies it. Evidence: Signal's CTO is quoted in the blog; they put two old bugs back into the code and the system proved the buggy version is not secure; the blog says the artifacts will be published as open source; the 4-week duration and the 1% figure are DeepMind's claims; 619 points on HN. Scores: effectiveness 5/5 in its domain, hype 3/5. Fit: low to medium for a general AI product, but the human–agent–formal-checker pattern transfers to other domains. Effort high. Recommendation: Watch.

## Sources

- [Introducing AlphaProof Code](https://deepmind.google/blog/introducing-alphaproof-code/)
