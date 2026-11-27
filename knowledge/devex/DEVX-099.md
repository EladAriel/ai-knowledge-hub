# DEVX-099: MCP Python SDK: upgrade and pass issuer= to your OAuth client (CVE-2026-115563, high: a malicious MCP server can redirect OAuth secrets)

## Summary

CVE-2026-115563 (high): a malicious MCP server can redirect your client's OAuth secrets to its own server. Upgrade `mcp`, and for machine-to-machine clients also pass `issuer=`, because upgrading alone changes nothing for them. Affects Python backends that connect to outside MCP servers over HTTP; servers and stdio clients aren't affected. Enterprise feasibility: High. Stage: Adopt. Effort: ~5 min.

## Details

- PoC:

```bash
pip install -U "mcp>=2.2.0"   # 1.x line: mcp>=1.30.0
```

```python
ClientCredentialsOAuthProvider(server_url=..., storage=..., client_id=..., client_secret=...,
    issuer="https://auth.example.com")
```

- Advisory: [GHSA-qx49-fqc8-xw99](https://github.com/advisories/GHSA-qx49-fqc8-xw99). Reported Nov 22. Expires Feb 20, 2027.
- Related: DEVX-049 (MCP HTTP session hijack advisories).

## Content

### MCP Python SDK: tell your OAuth client which login server to trust — Enterprise feasibility: High | Stage: Adopt

- **Problem → fix:** CVE-2026-115563 (high): a malicious MCP server can redirect your client's OAuth secrets to its own server. Upgrade `mcp`, and for machine-to-machine clients also pass `issuer=`, because upgrading alone changes nothing for them.
- **Why it matters:** Python backends that connect to outside MCP servers over HTTP could leak client secrets. Servers and stdio clients aren't affected.
- **Effort:** ~5 min.

```bash
pip install -U "mcp>=2.2.0"   # 1.x line: mcp>=1.30.0
```

```python
ClientCredentialsOAuthProvider(server_url=..., storage=..., client_id=..., client_secret=...,
    issuer="https://auth.example.com")
```

Advisory: [GHSA-qx49-fqc8-xw99](https://github.com/advisories/GHSA-qx49-fqc8-xw99) | expires: 2027-02-20

## Sources

- [GHSA-qx49-fqc8-xw99](https://github.com/advisories/GHSA-qx49-fqc8-xw99)
