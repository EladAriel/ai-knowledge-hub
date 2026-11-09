# EVAL-001: /claude-api build-eval + hillclimb

## Summary

Build an eval inside the codebase from real traces, then improve the app one patch at a time against held-out cases.

## Details

build-eval interviews you, gathers inputs (production transcripts > bug reports > your cases > generated), shows them for approval, picks the cheapest grader (code check or model+checklist), warns if baseline ~95%. ….

## Sources

- [Automating eval design and …](https://claude.dev/blog/automating-eval-design-and-hillclimbing/)
