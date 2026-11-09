# DEVX-019: /code-review as a pre-PR CI step

## Summary

Low effort keeps only the most confident findings, and the override stops Claude from starting reviews on its own. Credit: Claude Code docs.

## Content

**[/code-review as a pre-PR CI step](https://code.claude.com/docs/en/code-review-local)** runs a local review on any plan. Low effort keeps only the most confident findings, and the override stops Claude from starting reviews on its own. Effort ~5 min. Credit: Claude Code docs.
```bash
claude -p "/code-review low --max-findings 10 main...HEAD" --output-format json > review.json
# settings.json: { "skillOverrides": { "code-review": "user-invocable-only" } }
```

## Sources

- [code-review-local docs](https://code.claude.com/docs/en/code-review-local)
