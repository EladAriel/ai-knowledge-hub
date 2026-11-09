# DEVX-043: DBHub MCP server read-only bypass on MySQL/MariaDB (GHSA-j656-3hf2-fvjc)

## Summary

DBHub's SQL splitter treats '--' as a comment without whitespace, so 'SELECT 1--1;DROP TABLE victim' passes the read-only check and drops the table; fixed in @bytebase/dbhub 0.22.6. Lesson: MCP 'read-only mode' is a text filter; use a SELECT-only DB account.

## Details

Advisory public Nov 2 (medium), affects \< 0.22.6; PostgreSQL not affected; realistic attacker is prompt injection in content the agent reads. Fix shipped Jun 24, latest is 1.5.1, so only old pins are exposed.

## Sources

- [GHSA-j656-3hf2-fvjc](https://github.com/advisories/GHSA-j656-3hf2-fvjc)
- [DBHub v0.22.6](https://github.com/bytebase/dbhub/releases/tag/v0.22.6)
