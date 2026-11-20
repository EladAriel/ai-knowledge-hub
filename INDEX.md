# Index

## Files

| Index file | Item folder | Topic | ID prefix | Items |
|---|---|---|---|---|
| [knowledge/pipelines.md](knowledge/pipelines.md) | `knowledge/pipelines/` | AI Pipelines | `PIPE-NNN` | 34 |
| [knowledge/evals.md](knowledge/evals.md) | `knowledge/evals/` | AI Evals | `EVAL-NNN` | 43 |
| [knowledge/methods.md](knowledge/methods.md) | `knowledge/methods/` | AI Methods & Techniques | `METH-NNN` | 187 |
| [knowledge/devex.md](knowledge/devex.md) | `knowledge/devex/` | DevEx for AI | `DEVX-NNN` | 97 |
| [knowledge/tools-and-repos.md](knowledge/tools-and-repos.md) | `knowledge/tools-and-repos/` | Tools & Repos | `TOOL-NNN` | 51 |

Total: 412 items.

Ids are a per-topic prefix plus a 3-digit number. They are stable: never renumbered or reused. New items take the next free number.

## Topic index line format

```
- [METH-001](methods/METH-001.md) | <title> | <one-line summary>
```

One-line summaries are complete sentences (not cut mid-word).

## Item file schema (`knowledge/<topic>/<ID>.md`)

```
# METH-001: <title>

## Summary
<full plain-English summary; every substantive claim kept>

## Details
<full notes, numbers, steps, and caveats from the source digest>

## Content
<full body of the source digest: explanations, steps, examples, code snippets,
numbers, and caveats. May include subsections such as How it works / Example /
Caveats / Recommendation when those headings appear in the source.>

## Sources
- [label](https://…)
```

Items are curated notes about AI-development techniques and tools. They are starting points for evaluation, not verified production guidance. Prefer primary sources linked under Sources before adopting anything. Content aims to carry over the full substance of each source note (minus meta fields), translated to English where needed.
