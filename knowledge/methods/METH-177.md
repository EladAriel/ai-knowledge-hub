# METH-177: External Sandboxes: the agent stays outside and the code runs in a sandbox (Adopt as a pattern)

## Summary

Claude Code, Codex or Pi run on the machine as usual, but every command the agent runs is sent to a local API for an isolated Linux environment. There are three interchangeable implementations: v86 in WASM, Apple Containers, and Quicksand on QEMU. A proxy with an allow-list of sites injects API keys at the network level, so the agent never sees them. Recommendation: Adopt as a working pattern. Effort: low to medium. Simon Willison and Prime Radiant.

## Details

What is new: the split between the agent and the execution environment is a known pattern. The novelty is a shared protocol, so any of these agents can use any of the three sandboxes.

Evidence: there is code that runs, started with two `npx` commands (github.com/prime-radiant-inc/external-sandbox-container). There is no benchmark, and the authors present it explicitly as a prototype. Effectiveness 4/5, hype 2/5. Fit is high for any agent product that runs code or tools.

The same architecture, where the agent does not hold secrets and a proxy injects the keys, came up on Oct 24 in Google's Agent Compute Engine. The source note says this is settling as a standard, and it also continues the runtime-controls theme from guardscope (METH-166, Nov 14–15).

## Sources

- [External Sandboxes (Prime Radiant / Simon Willison)](https://blog.primeradiant.com/external-sandboxes-for-coding-agents/)
- [external-sandbox-container](https://github.com/prime-radiant-inc/external-sandbox-container)
