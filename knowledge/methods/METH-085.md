# METH-085: MCPGuard: spec-conformance gaps between the MCP spec and the official SDKs

## Summary

LLM-based tool that checks whether official MCP SDKs actually enforce the constraints the spec requires: structural comparison against the JSON Schema, checks of free-text rules, and a PoC built to confirm each finding.

## Details

Why new: existing conformance tools test live endpoints; this is the first to test the SDK itself. Evidence: 13 confirmed findings in the Python SDK (1.26.0) and 19 (rest of the item was cut off in the transcript).

## Sources

- [MCPGuard (arXiv)](https://arxiv.org/abs/2611.03662)
