# METH-091: Toward a Shared Organizational Cortex: claims layer with current-status and reasons

## Summary

Above raw records, store claims each with its reasons and whether it currently holds; when evidence changes, update each claim's status. nDCG@10 rose 0.081 over raw search and 0.053 over graph retrieval; eval plan was published before the run.

## Details

Caveats: small team that looks vendor-tied; data is old Enron email and Python design docs; repo has no license; core idea is classic truth-maintenance under a new name. Effort: high. Adopt for: Architects add a claims layer with an owner and a current-status field per claim; Product pilot it on one workflow with lots of decisions (e.g. pricing exceptions); Devs copy their format for writing the eval plan before running it.

## Sources

- [Toward a Shared Organizational Cortex (arXiv)](https://arxiv.org/abs/2611.05753)
- [eval code](https://github.com/withrobinhq/geometric-knowledge-paper-evals)
