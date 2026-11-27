# PIPE-036: Pipeline: parsing and chunking — chunk inside sections, keep tables whole

## Summary

Parsing and chunking angle (Nov 21): chunk inside sections, never across them. Store the full section path with each chunk, such as "Annual Report > Risk > FX", and put it in front of the text you embed. Keep tables whole as their own chunks.

## Details

This differs from earlier parsing and chunking angles (PIPE-009, PIPE-018, PIPE-027), which already talked about heading stacks and structure-aware packing. Today's practice is the hard rule: never cut across a section, put the section path in front of the embedded text, and keep each table as one chunk.

Who owns it: Architects define the section-path field and the rule that tables stay whole. Devs implement the chunker and the path prefix. Product reviews questions whose answers were split across chunks (see EVAL-016).

See also METH-190 (TETHER: use the table of contents as the heading source).

## Sources

- [TETHER: ToC-anchored parsing (METH-190)](https://arxiv.org/abs/2611.24960)
