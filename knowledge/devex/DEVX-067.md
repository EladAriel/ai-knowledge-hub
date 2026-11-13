# DEVX-067: Give every agent-built tool a named engineer owner (CODEOWNERS + PR checkbox)

## Summary

After traders' agent-built scripts reached daily use outside review, Goldman Sachs limited Claude Code and GitHub to engineers (strats keep access). Smallest useful copy: require a named engineering owner before anything agent-built touches production data. Feasibility High, stage Assess, ~10 min.

## Details

How: a CODEOWNERS entry plus one PR-template checkbox, so ownership lives in the repo. PoC: in .github/CODEOWNERS add /tools/ @your-org/platform-eng; in the PR template add '- [ ] Agent-built: named engineer owner: @____ (reviewed data access and entitlements)'.
Top HN comments point at the 'lethal trifecta' (client data, internet and internal network on one workstation) as the real risk.
Success metric: share of agent-built tools with an owner and review before first prod use. Seen in 2 sources (the article cites Bloomberg). Expires Feb 7, 2027.

## Content

### Give every agent-built tool a named engineer owner — Enterprise feasibility: High | Stage: Assess
- What changes: Goldman Sachs limited Claude Code and GitHub to engineers (strats keep access) after traders' agent-built scripts reached daily use outside review. The smallest useful copy of the lesson is to require a named engineering owner before anything agent-built touches production data.
- How it works: a `CODEOWNERS` entry plus one PR-template checkbox, so ownership lives in the repo instead of a policy PDF. Top HN comments point at the "lethal trifecta" (client data, internet and internal network on one workstation) as the real risk.
- Effort: ~10 min.
- PoC: in `.github/CODEOWNERS` add `/tools/ @your-org/platform-eng`, and in the PR template add `- [ ] Agent-built: named engineer owner: @____ (reviewed data access and entitlements)`.
- Success metric: share of agent-built tools with an owner and review before first prod use.
- Sources: [State of AI on Goldman's guidance](https://www.thestateofai.com/news/goldman-sachs-claude-code-traders-bankers), [HN thread, 724 points](https://news.ycombinator.com/item?id=50415628) | seen in 2 sources (the article cites Bloomberg) | expires Feb 7, 2027

## Sources

- [State of AI on Goldman's guidance](https://thestateofai.com/news/goldman-sachs-claude-code-traders-bankers)
- [HN 50415628](https://news.ycombinator.com/item?id=50415628)
- [State of AI on Goldman's guidance](https://www.thestateofai.com/news/goldman-sachs-claude-code-traders-bankers)
