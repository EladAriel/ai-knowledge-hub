# DEVX-044: AWS Serverless MCP Server \< 0.2.1 path traversal (CVE-2026-116635)

## Summary

A prompt-injected project name with traversal or an absolute path lets the agent read, or with write enabled overwrite, JSON files outside the deployment-status dir; fixed in 0.2.1, no workaround.

## Content

**[AWS Serverless MCP Server < 0.2.1: path traversal through the project name lets an agent read, or with write enabled overwrite, JSON files outside the deployment-status dir (CVE-2026-116635, AWS bulletin 2026-164-AWS)](https://aws.amazon.com/security/security-bulletins/2026-164-aws/)**
- **urls_extra:** ["https://nvd.nist.gov/vuln/detail/CVE-2026-116635", "https://github.com/awslabs/mcp/security/advisories/GHSA-r6mm-377j-qg8m", "https://pypi.org/project/awslabs.aws-serverless-mcp-server/0.2.1/"]
- **what_changed:** AWS bulletin 'Important', published Nov 2 at 13:30 PST (23:30 Israel time). NVD published it Nov 2 at 22:17Z (Nov 3 00:17 Israel time), CVSS 4.0 6.9. 'An actor who can influence the MCP agent' (i.e. prompt injection) can put traversal sequences or an absolute path in the project name. That reads JSON files outside the deployment-status directory, and creates or overwrites them where write access is enabled. Fixed in 0.2.1 (PyPI, Oct 30 20:56Z). AWS says there is no workaround. The global github.com/advisories page for the GHSA still 404s; the repo advisory page loads.
- **how_it_works:** Upgrade. Configs that launch it with `uvx ...@latest` pick up 0.2.1 on the next fresh resolve. Pinned versions or cached environments keep the bug until they're bumped.
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 10
- **poc_snippet:** # my composition (standard uv/pip)
pip show awslabs.aws-serverless-mcp-server 2>/dev/null | grep -i ^version   # vulnerable: < 0.2.1
grep -rn "aws-serverless-mcp-server" ~/.claude.json .mcp.json .cursor/mcp.json 2>/dev/null
uvx --refresh awslabs.aws-serverless-mcp-server@0.2.1 --help   # or pin >=0.2.1 in the MCP config
- **success_metric:** 0 configs pinning < 0.2.1. Write access stays off unless a team needs it.
- **org_challenge_if_relevant:** awslabs MCP servers are often added per developer. This is the second awslabs/mcp advisory in this radar this month (AWS API MCP Server CVE-2026-115413 was reported Oct 28), so it's worth one managed allowlist that pins awslabs versions.
- **project_health_if_relevant:** awslabs/mcp is AWS-maintained, with coordinated disclosure. ~16.8k PyPI downloads/week.
- **source_count:** 3
- **benefit_to_effort:** Medium (audience: AWS shops using the serverless MCP server)
- **why_enterprise_simple:** One version bump closes an agent-reachable file read/overwrite in an official AWS MCP server.

## Sources

- [AWS bulletin 2026-164-AWS](https://aws.amazon.com/security/security-bulletins/2026-164-aws/)
- [CVE-2026-116635](https://nvd.nist.gov/vuln/detail/CVE-2026-116635)
