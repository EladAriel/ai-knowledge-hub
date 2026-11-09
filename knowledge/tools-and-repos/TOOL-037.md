# TOOL-037: Repos: openfga/openfga, presidio (permissions + PII redaction for derived knowledge)

## Summary

openfga: relationship-based permission engine (Zanzibar style, CNCF, SDKs for Python/TS/Go/Java/.NET). presidio (formerly microsoft/presidio): finds and redacts personal data in text, images and structured data.

## Details

openfga: define relations between docs, folders, teams and users once; call ListObjects to filter retrieval up front and Check to confirm access on top results. Production grade, 6.1k stars, 553 forks, v1.22.1 Oct 28, Apache-2.0. Best for Architects. presidio: run it on summaries, memories and graph node text before they reach a wider audience than their sources. Production grade, 11.7k stars, pushed Nov 2, MIT. Best for Devs.

## Sources

- [openfga/openfga](https://github.com/openfga/openfga)
- [data-privacy-stack/presidio](https://github.com/data-privacy-stack/presidio)
