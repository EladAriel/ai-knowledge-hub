# METH-154: Deepnote's Agent Initiative Benchmark: agents help well but can't stay quiet

## Summary

12 models watch the Slack of a made-up company with 11 tools and 6 years of history, across 50 situations. In 40 the agent should help, and in 10 it should stay quiet because the issue is already handled. When help was needed, models sent a message 9 times out of 10; when silence was right, they held back only about 6 times out of 10, and the best did 8 out of 10. Released Nov 13. Effort: low to run the public tasks, medium to rebuild the test on your own data.

## Details

The two models that called tools most often scored lowest. The unneeded messages were well written, so a quality filter won't catch them. Unneeded messages cost about 1.8 times more than staying quiet. GPT-6.1 Sol scored 8.65 at $0.11 per task, while Claude Fable 5.2 scored 8.17 at $1.87. Caveats, from an outside critique: Gemini's perfect score on staying quiet came from runs that timed out, not from choosing to stay quiet; with only 10 silence tasks per model, the rankings between models aren't statistically meaningful; only 8 of the 50 tasks are public. Adopt for: Architects make "answer," "stay quiet," "ask" and "hand off" separate outcome types, and log a timeout as its own outcome, never as silence; Product, before turning on an always-on agent, track how often it posts about issues that are already resolved; Devs add 10–20 cases where the fix already lives in another tool, and check that no message gets sent. See also TOOL-049.

## Sources

- [Deepnote Agent Initiative Benchmark](https://deepnote.com/research/benchmark)
- [sysnote critique](https://sysnote.net/news/agent-initiative-benchmark-all-ten-of-gemini-4-argon-s-correct-silences-were-run)
