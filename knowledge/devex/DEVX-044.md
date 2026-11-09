# DEVX-044: AWS Serverless MCP Server \< 0.2.1 path traversal (CVE-2026-116635)

## Summary

A prompt-injected project name with traversal or an absolute path lets the agent read, or with write enabled overwrite, JSON files outside the deployment-status dir; fixed in 0.2.1, no workaround.

## Details

AWS bulletin 2026-164-AWS ('Important'), NVD CVSS 4.0 6.9. Configs launching with uvx ...@latest pick up 0.2.1 on the next fresh resolve; pinned or cached environments keep the bug.

## Sources

- [AWS bulletin 2026-164-AWS](https://aws.amazon.com/security/security-bulletins/2026-164-aws/)
- [CVE-2026-116635](https://nvd.nist.gov/vuln/detail/CVE-2026-116635)
