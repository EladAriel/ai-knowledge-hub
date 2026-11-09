# DEVX-043: DBHub MCP server read-only bypass on MySQL/MariaDB (GHSA-j656-3hf2-fvjc)

## Summary

DBHub's SQL splitter treats '--' as a comment without whitespace, so 'SELECT 1--1;DROP TABLE victim' passes the read-only check and drops the table; fixed in @bytebase/dbhub 0.22.6. Lesson: MCP 'read-only mode' is a text filter; use a SELECT-only DB account.

## Content

**[DBHub (Bytebase database MCP server) read-only mode bypass on MySQL/MariaDB, `SELECT 1--1;DROP TABLE victim`. GHSA-j656-3hf2-fvjc went public Nov 2; fixed in @bytebase/dbhub 0.22.6](https://github.com/advisories/GHSA-j656-3hf2-fvjc)**
- **urls_extra:** ["https://github.com/bytebase/dbhub/security/advisories/GHSA-j656-3hf2-fvjc", "https://github.com/bytebase/dbhub/pull/342", "https://github.com/bytebase/dbhub/commit/872bb338f7d31f6afe517a076ac3e3edafaaaf08", "https://github.com/bytebase/dbhub/releases/tag/v0.22.6"]
- **what_changed:** GitHub reviewed advisory, published Nov 2 at 17:57Z (19:57 Israel time), severity medium, affects < 0.22.6. DBHub's SQL splitter treats `--` as a comment even when no whitespace follows. MySQL and MariaDB don't (they read `1--1` as `1 - -1`). The read-only check validates the split statements but executes the original string, on a pool opened with `multipleStatements: true`. So `SELECT 1--1;DROP TABLE victim` passes the read-only check and drops the table. The realistic attacker is prompt injection in content the agent reads. PostgreSQL isn't affected. The fix (0.22.6) shipped Jun 24, 2026, and the current npm latest is 1.5.1, so only old pins are exposed. Now that the GHSA is public, Dependabot and npm audit will flag those pins.
- **how_it_works:** Upgrading removes the parser gap. The broader lesson: an MCP server's 'read-only mode' is a text filter. The real control is a database account that has only SELECT.
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 15
- **poc_snippet:** # my composition (standard npm / MySQL), not from the advisory
npm ls @bytebase/dbhub            # vulnerable: < 0.22.6 (latest is 1.5.1)
# MCP configs that pin a version: change to @bytebase/dbhub@latest or >= 0.22.6

-- defense in depth: give the agent a SELECT-only account instead of relying on --readonly
CREATE USER 'mcp_ro'@'%' IDENTIFIED BY '<secret>';
GRANT SELECT ON appdb.* TO 'mcp_ro'@'%';
- **success_metric:** 0 DBHub installs < 0.22.6. Every agent-facing DB DSN uses a SELECT-only account.
- **org_challenge_if_relevant:** DB MCP servers often run from personal `.mcp.json` / `.cursor/mcp.json` files that aren't in the SBOM. Grep the repos and managed MCP allowlists.
- **project_health_if_relevant:** Bytebase-maintained. ~34.8k npm downloads/week (Oct 26 to Nov 1). Patched four months before disclosure.
- **source_count:** 3
- **benefit_to_effort:** Medium-High (audience: teams with agents on MySQL/MariaDB through DBHub)
- **why_enterprise_simple:** One version check plus one GRANT turns the MCP-level 'read-only' promise into a database-enforced one.

## Sources

- [GHSA-j656-3hf2-fvjc](https://github.com/advisories/GHSA-j656-3hf2-fvjc)
- [DBHub v0.22.6](https://github.com/bytebase/dbhub/releases/tag/v0.22.6)
