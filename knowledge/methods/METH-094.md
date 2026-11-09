# METH-094: A thousand fewer paths to root (OpenAI): agent-pipeline lessons on path verification, harness re-check, and abandon budgets

## Summary

Autonomous agent pipeline (Scout, Analyst, Triage, ExploitDev, Patch) scanned the Linux kernel: verified 1,724 vulns, produced 948 local-priv-esc exploits and patches, ~$1.2M API cost. Three agent-engineering lessons with numbers, not the cyber itself.

## Details

1) 20 of 200 'successful' exploits got root via a different vuln than assigned — verify the path to the result, not only the result. 2) A techniques/skills layer raised GPT-5.5 Cyber . Effort: low. Recommendation: Adopt the patterns. Harness theme continues after Oct 18, Oct 30, Nov 3.

## Content

**1. [A thousand fewer paths to root (OpenAI)](https://openai.com/index/a-thousand-fewer-paths-to-root/)** ([HN discussion](https://news.ycombinator.com/item?id=50372929), 292 points)
- **What it is:** An autonomous pipeline of agents (Scout, Analyst, Triage, ExploitDev, Patch) that scanned the Linux kernel. It verified 1,724 vulnerabilities, produced 948 local privilege escalation exploits, and produced patches. Cost: About $1.2 million in API.
- **Why new:** Not the cyber itself, but three lessons of agent engineering with numbers:
  1. 20 out of 200 "successful" exploits obtained root through a different vulnerability than the one assigned to them. You need to verify the path to the result, not just the result.
  2. Techniques and skills layer improved GPT-5.5 Cyber ​​from 76.2% to 88.9%, but in the stronger model added only 1.5 points. The orchestration should be re-examined in each model generation.
  3. Failed attempts cost an average of $3,922, compared to $360 for a successful attempt. You should define waiver conditions.
- **Evidence:**
  - OpenAI self-reporting, with cost breakdown for each step.
  - According to the post, 61 vulnerabilities have already been fixed upstream and 43 are in staging.
  - The code, model and list of vulnerabilities have not been published. HN commenters requested the list.
- **Scores:** Effectiveness 4/5, Hype 3/5.
- **Fit:** High as a template. The lessons on path validation, concession budgeting, and harness reexamination apply to any agent that performs operations. **low** effort.
- **Recommendation: Adopt** for patterns. The subject of the harness returns, after 18.10, 30.10 and 3.11.

## Sources

- [OpenAI post](https://openai.com/index/a-thousand-fewer-paths-to-root/)
- [HN (292 points)](https://news.ycombinator.com/item?id=50372929)