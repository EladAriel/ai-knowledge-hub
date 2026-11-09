# DEVX-027: Enforce token audience on HTTP MCP servers you host

## Summary

The MCP Python SDK advisories now have CVE IDs, so Dependabot and pip-audit will flag old 'mcp' versions.

## Content

### 3. Enforce token audience on HTTP MCP servers you host — Enterprise feasibility: High | Stage: Adopt
- **What changed:** The MCP Python SDK advisories now have CVE IDs, so Dependabot and pip-audit will flag `mcp` below 1.30.0 or 2.2.0. The catch is that [CVE-2026-116684](https://github.com/advisories/GHSA-w4fh-qvv9-3v23) (accepting tokens issued for another app) is opt-in: upgrading alone changes nothing. The same bug class hit the [AWS API MCP Server](https://github.com/awslabs/mcp/security/advisories/GHSA-4prq-p2x5-w9fh) (CVE-2026-115413, high, fixed in 1.6.0).
- **How:** Set `validate_token_resource=True` and have your verifier return `AccessToken.resource`. Doing only the first part makes every request fail with 401. This only matters for HTTP servers with bearer auth, not stdio ones.
- **Effort:** ~30 min per server.
- **PoC** (from the [SDK auth docs](https://github.com/modelcontextprotocol/python-sdk/blob/main/docs/run/authorization.md)):
```python
auth=AuthSettings(
    issuer_url=AnyHttpUrl("https://auth.example.com"),
    resource_server_url=AnyHttpUrl(RESOURCE),
    required_scopes=["notes:read"],
    validate_token_resource=True,
)
```
For the AWS server 1.6.0 or newer, set `AUTH_AUDIENCE=my-mcp-server` (or `AUTH_CLIENT_ID` for Cognito).
- **Success metric:** A token minted for another app in the same tenant gets a 401 from every internal MCP server.
- **Sources:** [GHSA-w4fh-qvv9-3v23](https://github.com/advisories/GHSA-w4fh-qvv9-3v23), [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-115413), [aws-api-mcp-server 1.6.0](https://pypi.org/project/awslabs.aws-api-mcp-server/1.6.0/). Seen in 3 sources.

## Sources

- [GHSA-w4fh-qvv9-3v23](https://github.com/advisories/GHSA-w4fh-qvv9-3v23)
- [AWS API MCP Server](https://github.com/awslabs/mcp/security/advisories/GHSA-4prq-p2x5-w9fh)
- [SDK auth docs](https://github.com/modelcontextprotocol/python-sdk/blob/main/docs/run/authorization.md)
- [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-115413)
- [aws-api-mcp-server 1.6.0](https://pypi.org/project/awslabs.aws-api-mcp-server/1.6.0/)
