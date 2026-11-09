# DEVX-027: Enforce token audience on HTTP MCP servers you host

## Summary

The MCP Python SDK advisories now have CVE IDs, so Dependabot and pip-audit will flag old 'mcp' versions.

## Details

The catch is that CVE-2026-116684 (accepting tokens issued for another app) is opt-in: upgrading alone changes nothing. The same bug class hit the AWS API MCP Server (CVE-2026-115413, high, fixed in 1.6.0). ….

## Sources

- [GHSA-w4fh-qvv9-3v23](https://github.com/advisories/GHSA-w4fh-qvv9-3v23)
- [AWS API MCP Server](https://github.com/awslabs/mcp/security/advisories/GHSA-4prq-p2x5-w9fh)
- [SDK auth docs](https://github.com/modelcontextprotocol/python-sdk/blob/main/docs/run/authorization.md)
