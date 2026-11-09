# METH-043: OPAL: Reactive Optimizers (MIT)

## Summary

An agent (Claude Code) observes the training dynamics, and during the run rewrites two files: 'updater.py' (the update rule) and 'analysis.py' (what to measure). The code came out on 21.10.

## Content

### 2. [OPAL: Reactive Optimizers (MIT)](https://xingjianbai.com/reactive-optimizers/)
- **What it is:** A one-line wrapper for the PyTorch optimizer. An agent (Claude Code) observes the training dynamics, and during the run rewrites two files: `updater.py` (the update rule) and `analysis.py` (what to measure). [The code](https://github.com/xingjian-bai/opal) was released on 21.10.
- **Why new:** The goal is the optimization code itself, within one run, without meta-learning. This is neither hyperparameter tuning nor AutoML, and the authors note that the idea builds on previous work. There are safety mechanisms: a trial of 20 steps before each change of program, and return ...n- **Recommendation: Pilot** in a harness with a small model. State the failure without citing the action again.

---

## Sources

- [OPAL: Reactive Optimizers (MIT)](https://xingjianbai.com/reactive-optimizers/)
- [the code](https://github.com/xingjian-bai/opal)
