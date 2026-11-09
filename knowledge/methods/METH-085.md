# METH-085: MCPGuard: spec-conformance gaps between the MCP spec and the official SDKs

## Summary

LLM-based tool that checks whether official MCP SDKs actually enforce the constraints the spec requires: structural comparison against the JSON Schema, checks of free-text rules, and a PoC built to confirm each finding.

## Content

**2. [MCPGuard: compatibility gaps between the MCP specification and the official SDKs](https://arxiv.org/abs/2611.03662)**
- **What it is:** An LLM-based tool that checks if the official MCP SDKs really enforce the constraints that the specification requires. It compares a structure against the JSON Schema, checks for rules written in free language, and builds a PoC to confirm any findings.
- **Why new:** The existing compatibility tools test live endpoints, and this is the first to test the SDK itself.
- **Evidence:**
  - Found 13 verified findings in the Python SDK (version 1.26.0) and 19...A:** 1 stable interface, 1 cheap model and a small sample.
- **Scores:** Effectiveness 3/5, Hype 1/5.
- **Compatibility:** For any Enterprise product that sells "agent instead of automation". **Low** effort: agent only when the interface changes, or as a backup to RPA.
- **Recommendation: Adopt** as a baseline. This connects to the Coordination Tax from 30.10: first compare against the simple solution.

## Sources

- [MCPGuard (arXiv)](https://arxiv.org/abs/2611.03662)
