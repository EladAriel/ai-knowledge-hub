# EVAL-001: /claude-api build-eval + hillclimb

## Summary

Build an eval inside the codebase from real traces, then improve the app one patch at a time against held-out cases.

## Details

build-eval interviews you, gathers inputs (production transcripts > bug reports > your cases > generated), shows them for approval, picks the cheapest grader (code check or model+checklist), warns if baseline ~95%. hillclimb splits train/held-out, proposes one patch per round, keeps it only if both improve, reverts otherwise, reports test results with confidence intervals. Results: 44-ticket support benchmark held-out 78.6% -> 90.5% at ~1/5 cost; claude-api skill eval 66% -> ~88%. Verdict: only if you have a Claude-backed feature with real traffic.

## Content

- The claude-api skill now has `/claude-api build-eval`, which builds an eval inside your codebase, and `/claude-api hillclimb`, which improves your app against that eval one change at a time. The trade-off is setup time and tokens up front, in exchange for prompt and model changes you can actually trust.

- If your app has Claude prompts, tools or skills inside it, this is how you prove a tweak or model swap really helped and didn't just overfit to your test cases.

- `build-eval` interviews you and gathers inputs from production transcripts, then bug reports, then cases you write, then generated ones, and shows them on a page for you to approve. It then picks the cheapest grader that fits, either a code check or a second model scoring against a checklist, and warns you if your starting score is already around 95%.

- `hillclimb` randomly splits your cases into a training set and a held-out test set, and proposes one patch per round. It keeps a patch only when both sets improve, and reverts it if only the training set improves or the score drops. The final report gives test results with confidence intervals.

- Next move: run `claude update`, then run `/claude-api build-eval` on one feature using real traces.

- Should you try it? Only if you already have a Claude-backed feature with real traffic. Until then, skip it.

Example
A React + TypeScript app with a Python endpoint that sorts support emails into labels.
`/claude-api build-eval` → it pulls 30 real tickets from logs and you add 5 hand-written edge cases → a code grader checks each label against the fixed set → baseline score → `/claude-api hillclimb` with the goal "lower cost while accuracy holds" → it tries trimming the prompt, lowering effort, and switching to Sonnet → it keeps only the patches that also improve the held-out tickets.

- On a 44-ticket support benchmark, held-out accuracy went from 78.6% to 90.5% at about a fifth of the cost.
- The claude-api skill's own eval went from 66% to about 88% by adding missing features and fixing outdated API usage.
- Hillclimbing a skill's description can raise how often the skill gets used.

[Automating eval design and hillclimbing with Claude](https://claude.dev/blog/automating-eval-design-and-hillclimbing/)

## Sources

- [Automating eval design and hillclimbing with Claude](https://claude.dev/blog/automating-eval-design-and-hillclimbing/)