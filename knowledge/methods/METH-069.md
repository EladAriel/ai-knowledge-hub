# METH-069: LlamaIndex Document Parsing Protocol (DPP) draft 0.1

## Summary

140 rules for what a correct parse looks like; e.g. tables keep multi-row headers, written as HTML with cells that span columns.

## Content

**2. [LlamaIndex Document Parsing Protocol (DPP), draft 0.1](https://www.llamaindex.ai/blog/introducing-the-document-parsing-protocol)**
- **What it is:** 140 rules for what a correct parse looks like. For example:
  - Tables keep their multi-row headers, written as HTML with cells that span columns.
  - Empty... evidence together, before buying anything smarter.

**[run-llama/document_parsing_protocol](https://github.com/run-llama/document_parsing_protocol)** holds the DPP rules, example pages and a Claude skill.
- What to borrow: turn the rules into test cases for your parser.
- Maturity: early, with 22 stars, created Oct 19, MIT license. It's a spec, not a library.
- Best for: Architects, who own the parsing contract.

## Sources

- [LlamaIndex DPP blog](https://www.llamaindex.ai/blog/introducing-the-document-parsing-protocol)
- [run-llama/document_parsing_protocol](https://github.com/run-llama/document_parsing_protocol)
