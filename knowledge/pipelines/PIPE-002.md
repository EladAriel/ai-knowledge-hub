# PIPE-002: Claude Code team's layered code review

## Summary

Stack automated checks so humans spend attention only where risk is; merged PRs doubled while revert rate fell >40%.

## Details

Flow: change -> Claude runs tests/build/lint -> fresh-context subagent reviews diff -> required CI -> parallel AI bug hunters with verifier agents voting -> separate security review -> risk classifier sets 0/1/2 human approvals ….

## Sources

- [How the Claude Code team …](https://claude.dev/blog/solving-code-review-at-anthropic/)
- [HN](https://news.ycombinator.com/item?id=50122951)
- [Simon Willison](https://simonwillison.net/2026/Oct/16/code-review/)
- [customize docs](https://code.claude.com/docs/en/code-review-customize)
