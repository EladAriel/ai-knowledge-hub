# METH-190: TETHER: use the table of contents as the skeleton when parsing long docs

## Summary

Parsers guess section depth from font size and layout. On designed PDFs, such as annual reports, ESG reports and manuals, they get the headings wrong, so chunks lose their section context. TETHER reads the table of contents first and builds a document skeleton from it with a multimodal model, then attaches each content block to the matching table-of-contents entry. No training needed. The paper reports better hierarchy recovery than Docling, Marker, MinerU and big general models, with about 90% fewer tokens than extracting the whole document in one go. The paper says code is on GitHub, but the repo could not be found, so treat this as a pattern for now. Next step: if a doc has a table of contents, use it as the heading source, and only fall back to layout guesses when it doesn't. For: devs and architects. arXiv 2611.24960.

## Details

Reported Nov 21. This is not METH-027 (Tether: withdraw memories when their sources break), which is a different idea with a similar name.

Complements today's parsing practice in PIPE-036.

## Sources

- [TETHER (ToC-anchored parsing)](https://arxiv.org/abs/2611.24960)
