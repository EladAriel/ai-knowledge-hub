# DEVX-093: Give Claude a recorded verify recipe so it smoke-tests before each commit

## Summary

The Claude Code team's Nov 16 verification post says running the app end to end beats tests alone. Their setup is a `verify` skill per repo. Since 2.1.286, a project or personal skill named `verify` (or `simplify`) makes Claude run it right before every commit, except for docs and test changes. `/run-skill-generator` records the build and launch steps once, and `/verify` saves them to `.claude/skills/verify/SKILL.md`. Enterprise feasibility: Medium. Stage: Trial. Effort: about 20 minutes.

## Details

How the team thinks about verification, from the claude.dev post: give agents cheap ways to prove their work — end-to-end, property, and differential tests, plus a fast verify skill. The cost is upfront work, and flaky or slow tests teach the agent to rerun them instead of fixing the code. Verification is what lets you run many agents in parallel instead of reading every diff yourself. In their internal tests, adding a separate grader raised task success by up to 10 points. Flow: change → verify skill boots and drives the app → tests, build, and lint run → still failing after 3 rounds → a human steps in. Gates like REVIEW.md are read from the base branch so a change can never edit its own check, and a new commit gate runs in observe mode before it starts enforcing.

Practical one-liners: round-trip (encode then decode returns the original); invariant (an account balance never goes negative); idempotency (running a migration or retry twice has the same effect as once); differential test (old and new systems get the same random inputs, and any output difference is a bug); a diff-triggered checklist of only the 3 to 10 reliability items whose trigger matches the diff; a pattern that shows up in 2 or more PRs becomes a REVIEW.md rule once a human approves it. The post says to try it: it is cheap, and it pays off on the next agent task.

HN commenters warn that running it on every change costs tokens, so start with one repo. Success metric: the revert rate and the "broke on launch" PR comments for that repo, measured over the 2 weeks before and after. Seen in 3 sources, plus the claude.dev post. Expires Feb 16, 2027.

Ready-to-use mod (observe-mode commit log, about 3 minutes, needs `jq`): the first step of the team's "off, observe, enforce" commit gate. It logs every `git commit` Claude makes, without blocking anything. It prints no decision, so the 2.1.326 hook-block change can't make it block. In `~/.claude/settings.json`:
```json
{ "hooks": { "PreToolUse": [ { "matcher": "Bash", "hooks": [ { "type": "command", "if": "Bash(git commit *)",
  "command": "jq -c '{ts:(now|todate), session:.session_id, cmd:.tool_input.command}' >> ~/.claude/commit-log.jsonl" } ] } ] } }
```
The commit-log command is an adaptation of the docs' hook `if` example.

## Sources

- [Verification post (claude.dev)](https://claude.dev/blog/how-the-claude-code-team-thinks-about-verification/)
- [skills docs: checks before each commit](https://code.claude.com/docs/en/skills#run-your-checks-before-each-commit)
- [HN thread (281 points)](https://news.ycombinator.com/item?id=50529612)
