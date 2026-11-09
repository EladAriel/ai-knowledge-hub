# TOOL-032: Repo: xberg-io/xberg (formerly Kreuzberg)

## Summary

Extracts text, tables and metadata from 100+ file formats, with OCR and code-aware chunking; library, CLI, REST API or MCP server, CPU only.

## Content

**[xberg-io/xberg](https://github.com/xberg-io/xberg)**, formerly Kreuzberg, pulls text, tables and metadata out of more than 100 file formats. It includes OCR and chunking that understands code.
- It runs as a library, a command-line tool, a REST API or an MCP server, on CPU only.
- What to borrow:
  - `pip install xberg`, then its `extract` and `chunk` commands.
  - Caching by content hash, so unchanged files aren't processed twice.
  - Per-file timeouts.
- Maturity: about 9.5k stars, pushed today, v1.3.10 released Oct 13, MIT license. Several projects depend on it, mostly under the old Kreuzberg name.
- Best for: Devs.

## Sources

- [xberg](https://github.com/xberg-io/xberg)
