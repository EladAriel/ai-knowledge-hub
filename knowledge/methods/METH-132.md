# METH-132: DEPUTYBENCH: missing permission info is the bigger risk

## Summary

Across 12 models, agents took restricted actions more often when permission info was missing (10.3%) than when access was clearly denied (3.5%).

## Details

Limit they state: most of those failures came from 4 privacy tasks that needed consent or complete counts. Effort: medium. Adopt for: Architects—if the agent can't verify permission, deny. Enforce that in code, not in the prompt; Product—show users a clear "stopped, couldn't verify access" result; Devs—add tests that hide the permission record and check that the agent stops. arXiv 2611.13355.

## Sources

- [DEPUTYBENCH (arXiv)](https://arxiv.org/abs/2611.13355)
