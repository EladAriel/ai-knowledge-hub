# METH-042: Large-scale formal verification with LLM (Anthropic and Theorem)

## Summary

Claude wrote proofs in Rocq at the RISC-V binary code level.

## Content

### 1. [Large-scale formal verification with LLM (Anthropic and Theorem)](https://www.anthropic.com/research/formal-verification)
- **What it is:** Claude wrote proofs in Rocq at the RISC-V binary code level. The proofs show no crash for any input up to 64MB, at 239 entry points of 123 OSS-Fuzz libraries. Along the way Claude found and fixed bugs that phasing hadn't caught in years.
- **Why new:** Such formal verification work used to require expert man-years. Here it was done autonomously, to the extent of about 180 million lines of proof, and on the binary itself without rewriting the code. [In the appendix](https://www-cdn.anthropic.com/files/4zrzovbb/website/6867eadf760258fa8b42a504600cd3c036d16358.pdf) there is also a complementary experiment: a Python interpreter in Rust validated on Verus. Out of 7 intentionally injected bugs, 5 were randomly tested, and all 7 broke the proof.
- **Evidence:** Proven, with a proof checker and detailed numbers. The limitations are stated: single-threaded static binary, RISC-V, and Linux model. "Verified" does not mean "bug free". Checking one proof takes between 30 minutes and several CPU hours.
- **Scores:** Effectiveness 4/5, Hype 2/5.
- **Fit:** High for infrastructure code and security layers of agent products, low for RAG and organizational assistants. **high** effort.
- **Recommendation: Watch.** Pilot only on a single critical C library.
- **Repeat:** Code that was checked automatically, after the code review of the Claude Code team from 17.10.

## Sources

- [Large-scale formal verification with LLM (Anthropic and Theorem)](https://www.anthropic.com/research/formal-verification)
- [in the appendix](https://www-cdn.anthropic.com/files/4zrzovbb/website/6867eadf760258fa8b42a504600cd3c036d16358.pdf)
