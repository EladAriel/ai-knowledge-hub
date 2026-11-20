# EVAL-042: Eval: content-gap mining from failed queries (gap rate and time-to-close)

## Summary

A weekly audit of production queries that failed visibly (zero or low-score retrieval, abstentions, thumbs-down, escalations, user corrections). They are grouped into clusters, each cluster gets one cause label, and closed gaps become new golden questions. The outputs are a gap rate and a time-to-close. Effort: start in under a day.

## Details

Steps (Nov 18):
1. Sample last week's failed queries (for example all abstentions + thumbs-down + top-k max score below threshold; cap at about 300).
2. Embed and cluster them (HDBSCAN or k-means), and name each cluster with an LLM using 5 examples.
3. Give each cluster exactly one label: missing-content / stale-content / connector-gap / permission / retrieval-miss / out-of-scope. Rule of thumb: if the answer exists in the index, it's a retrieval-miss (or permission, if the user's ACL hides it). If it exists only in an unconnected system, it's a connector-gap.
4. Open one ticket per cluster for the owning team, and record the open date.
5. When a ticket is fixed, re-run the cluster's example queries. If they pass, add 1–3 of them to the golden set.
6. Track gap rate (failed-query clusters per 1k queries), the share by label, and median time-to-close per label.

Start in under a day: export one week of logs with thumbs-down or abstain flags, cluster them in a notebook, then hand-label the top 15 clusters in a spreadsheet. That spreadsheet is the first gap backlog.

What it catches: missing or stale docs, unconnected sources, wrong ACL scoping that looks like "no answer", retrieval misses where the content exists, and scope creep. Most of these never show up in a static golden set.

Who runs it: Product runs the weekly triage and owns labels and routing. Devs build the export, clustering job and re-run step. Architects review the label mix each quarter: if connector-gap or permission keeps growing, that is a platform problem, not a content problem.

## Sources

- No external link was recorded for this eval itself. Related public sources (see PIPE-033 and TOOL-050):
- [Intercom Fin content-gap suggestions](https://intercom.help/fin4all/en/articles/11420114-use-ai-powered-content-suggestions-to-improve-fin)
- [HelpCenterKit: find content gaps](https://helpcenterkit.com/use-cases/find-content-gaps)
- [Mind the Gap (re-answer after fix)](https://arxiv.org/abs/2611.23142)
- [OCNAI/kebivo](https://github.com/OCNAI/kebivo)
