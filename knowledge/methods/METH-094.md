# METH-094: A thousand fewer paths to root (OpenAI): agent-pipeline lessons on path verification, harness re-check, and abandon budgets

## Summary

Autonomous agent pipeline (Scout, Analyst, Triage, ExploitDev, Patch) scanned the Linux kernel: verified 1,724 vulns, produced 948 local-priv-esc exploits and patches, ~$1.2M API cost. Three agent-engineering lessons with numbers, not the cyber itself.

## Details

1) 20 of 200 'successful' exploits got root via a different vuln than assigned — verify the path to the result, not only the result. 2) A techniques/skills layer raised GPT-5.5 Cyber from 76.2% to 88.9%, but on a stronger model added only 1.5 points — re-evaluate orchestration each model generation. 3) Failed attempts cost ~$3,922 on average vs $360 for successes — define abandon conditions. Evidence: OpenAI self-report with per-stage costs; 61 vulns already fixed upstream, 43 in staging; code/model/vuln list not published. Scores: effectiveness 4/5, hype 3/5. Fit: high as a template for any action-taking agent.

## Sources

- [OpenAI post](https://openai.com/index/a-thousand-fewer-paths-to-root/)
- [HN (292 points)](https://news.ycombinator.com/item?id=50372929)
