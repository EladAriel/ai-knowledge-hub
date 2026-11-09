# DEVX-051: GitBook breach (AI-agent-driven attack): rotate GitBook tokens and re-auth its MCP server

## Summary

GitBook says an attacker using AI agents got some infrastructure credentials on Nov 2; integration tokens, Git Sync secrets, API tokens and Assistant questions may have been accessed. Rotate GitBook API, third-party and integration secrets, and re-authenticate the GitBook MCP server.

## Content

**[GitBook breach (AI-agent-driven attack): rotate GitBook API, integration and Git Sync secrets, and re-authenticate the GitBook MCP server](https://www.gitbook.com/status/security-incident-2026-11-03)**
- **urls_extra:** ["https://news.ycombinator.com/item?id=50354336", "https://x.com/AxoraSecurity/status/2117798045543022615"]
- **what_changed:** GitBook says an attacker 'using AI agents' got some of its infrastructure credentials at 19:00 CET on Nov 2 (20:00 Israel time). GitBook took the app offline, rotated all of its own secrets and invalidated every customer API token. In the Nov 3 16:21 CET update (17:21 Israel time), it says the attacker may have accessed integration tokens, Git Sync secrets, API tokens and visitors' GitBook Assistant questions. GitBook has found no evidence that content was modified. HN thread: 153 points.
- **how_it_works:** Customer actions, quoted from GitBook: rotate GitBook API tokens; rotate third-party tokens and secrets used to connect tools to GitBook; rotate secrets of published integrations; 're-authenticate' the GitBook MCP server.
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 30
- **poc_snippet:** # my composition: find where GitBook credentials live, then rotate them per GitBook's list
grep -rIl -i 'gitbook' .github/ .claude/ .cursor/ ~/.claude.json [local path removed] 2>/dev/null
# GitHub/GitLab: review and re-issue the GitBook Git Sync app or deploy key, and check audit logs since Nov 2 18:00Z
# Claude Code / Cursor: remove and re-add the GitBook MCP server so it gets a fresh OAuth token
- **success_metric:** Every GitBook-linked token or secret rotated within 48 h. No Git Sync pushes since Nov 2 that nobody can account for.
- **org_challenge_if_relevant:** Git Sync credentials can write to the docs repos, so check audit logs on the connected GitHub/GitLab repos as well. The full post-mortem is still pending.
- **project_health_if_relevant:** Vendor incident notice; post-mortem promised.
- **source_count:** 3
- **benefit_to_effort:** Medium-High (audience: orgs using GitBook)
- **why_enterprise_simple:** A token-rotation checklist from the vendor, with the MCP re-auth step included.

## Sources

- [GitBook security incident](https://www.gitbook.com/status/security-incident-2026-11-03)
- [HN thread](https://news.ycombinator.com/item?id=50354336)
