# EVAL-016: Eval: answer-span containment and chunk integrity

## Summary

Check whether each gold answer span sits whole inside one chunk and in the retrieved top-k; ….

## Details

1) 50-100 gold Q&A with answer offsets in the parsed text (+ table and page-break questions). 2) locate_span: exact then whitespace-normalized; not found = parse-fidelity failure. 3) Keep (doc_id,start,end) per chunk. ….

## Sources

- [span-to-chunk mapping](https://arxiv.org/abs/2610.31606)
