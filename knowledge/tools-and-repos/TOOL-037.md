# TOOL-037: Repos: openfga/openfga, presidio (permissions + PII redaction for derived knowledge)

## Summary

openfga: relationship-based permission engine (Zanzibar style, CNCF, SDKs for Python/TS/Go/Java/.NET). presidio (formerly microsoft/presidio): finds and redacts personal data in text, images and structured data.

## Content

**[openfga/openfga](https://github.com/openfga/openfga)** is a permission engine where access follows relationships, in the style of Google's Zanzibar. It's a CNCF project with SDKs for Python, TypeScript, Go, Java and .NET.
- What to borrow: define the relations between docs, folders, teams and users once. Then call `ListObjects` to filter retrieval up front, and `Check` to confirm access on the top results.
- Maturity: production grade, 6.1k stars, 553 forks, v1.22.1 released Oct 28, Apache-2.0.
- Best for: Architects.

**[data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio)**, formerly microsoft/presidio, finds and redacts personal data in text, images and structured data.
- What to borrow: run it on summaries, memories and graph node text before they reach a wider audience than their sources.
- Maturity: production grade, 11.7k stars, pushed Nov 2, MIT license.
- Best for: Devs.

## Sources

- [openfga/openfga](https://github.com/openfga/openfga)
- [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio)
