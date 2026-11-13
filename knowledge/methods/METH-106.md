# METH-106: SUMONE: a plug-in summarizer for long agent sessions

## Summary

A small 2B model trained to compress an agent's history without task labels. Vs full history: estimated cost fell ~78% on DeepSearchQA and ~75% on SWE-bench Verified, with scores down only 0.04; same model worked across agent frameworks.

## Details

Caveat: cost figures are estimates—measure on your own sessions. Effort: medium. Adopt for: Architects make history compression its own swappable module; Product track cost per session with compression on/off; Devs try a small summarizer before paying for bigger context windows.

## Sources

- [SUMONE (arXiv)](https://arxiv.org/abs/2611.06445)
