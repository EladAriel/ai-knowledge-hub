# METH-091: Toward a Shared Organizational Cortex: claims layer with current-status and reasons

## Summary

Above raw records, store claims each with its reasons and whether it currently holds; when evidence changes, update each claim's status. nDCG@10 rose 0.081 over raw search and 0.053 over graph retrieval; eval plan was published before the run.

## Content

**2. [Toward a Shared Organizational Cortex](https://arxiv.org/abs/2611.05753)** ([eval code](https://github.com/withrobinhq/geometric-knowledge-paper-evals))
- **The idea:** above the raw records, it stores claims, each with its reasons and whether it currently holds. When evidence changes, a system updates each claim's status.
- **Results:** ranking quality (nDCG@10) went up 0.081 over searching raw records and 0.053 over graph-based retrieval. They published their eval plan before running it, which is rare.
- **Caveats:**
  - It's a small team that looks tied to a vendor.
  - The data is old Enron email and Python design docs.
  - The repo has no license.
  - The core idea is the classic truth-maintenance system from early AI under a new name.
- Adopt for:
  - *Architects:* add a claims layer, with an owner and a current-statuscurrent-status field per claim.
  - *Product:* pilot it on one workflow with lots of decisions (for example pricing exceptions).
  - *Devs:* copy their format for writing the eval plan before running it.

## Sources

- [Toward a Shared Organizational Cortex (arXiv)](https://arxiv.org/abs/2611.05753)
- [eval code](https://github.com/withrobinhq/geometric-knowledge-paper-evals)
