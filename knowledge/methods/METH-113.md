# METH-113: Context Mode 2.0: turning a bug backlog into tests

## Summary

A plugin for coding agents that stores raw tool output in a local database and gives the agent only the parts it asks for. The process lesson: they went through 351 open issues and PRs, turned 124 real bugs into tests, and now run 2,071 tests in CI. Claimed 99.4% context saving is from their own benchmark.

## Details

Effort: low. Adopt for: Architects keep raw tool and connector output out of the prompt, stored where the agent can search it; Product go through the backlog once so every confirmed failure gets a test; Devs for every connector bug write one test. Repo already listed under TOOL-040 (mksglu/context-mode; Elastic 2.0 license warning).

## Sources

- [Context Mode 2.0](https://contextmode.ai/blog/context-mode-2-0)
- [context-mode repo](https://github.com/mksglu/context-mode)
