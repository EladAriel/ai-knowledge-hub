# DEVX-051: GitBook breach (AI-agent-driven attack): rotate GitBook tokens and re-auth its MCP server

## Summary

GitBook says an attacker using AI agents got some infrastructure credentials on Nov 2; integration tokens, Git Sync secrets, API tokens and Assistant questions may have been accessed. Rotate GitBook API, third-party and integration secrets, and re-authenticate the GitBook MCP server.

## Details

GitBook took the app offline, rotated its secrets and invalidated all customer API tokens; no evidence content was modified; post-mortem pending.

## Sources

- [GitBook security incident](https://www.gitbook.com/status/security-incident-2026-11-03)
- [HN thread](https://news.ycombinator.com/item?id=50354336)
