# DEVX-049: MCP HTTP session hijack: C# SDK (GHSA-x863-g495-4cjc) and SurrealDB MCP (CVE-2026-121419), plus a cross-user replay test

## Summary

Both bound a session to an identity several users share (null claim, or the access-method name), so a user holding another's Mcp-Session-Id could take over. Upgrade ModelContextProtocol.AspNetCore to >= 2.3.1 / 1.4.2 and SurrealDB to >= 3.3.0, and test every HTTP MCP server by replaying user A's session with user B's token (expect 403).

## Details

C# SDK: high, CVSS 7.5, published Nov 3; affected >= 0.1.0-preview.9 \< 1.4.2 and >= 2.0.0-preview.1 \< 2.3.1. Fix fails closed: principals without NameIdentifier/sub/UPN get 403 on stateful sessions; add an IClaimsTransformation that maps your own ID claim to NameIdentifier (from the SDK docs). On 1.4.2 OAuth discovery validates PKCE and metadata issuer; metadata-free 2025-03-26 servers must advertise S256 or opt in to AllowLegacyOAuthMetadataFallback. SurrealDB 3.1.0 to \< 3.3.0: BoundSubject used the access-method name for JWT/Bearer DEFINE ACCESS, letting a viewer act with an editor's roles (CVSS 4.0 8.6). Instatic CVE-2026-121458 is a third same-day case of MCP path having weaker authz than the API.

## Sources

- [GHSA-x863-g495-4cjc](https://github.com/modelcontextprotocol/csharp-sdk/security/advisories/GHSA-x863-g495-4cjc)
- [CVE-2026-121419](https://nvd.nist.gov/vuln/detail/CVE-2026-121419)
- [SurrealDB advisory](https://github.com/surrealdb/surrealdb/security/advisories/GHSA-pgh9-49q4-hqcx)
- [NuGet 2.3.1](https://www.nuget.org/packages/ModelContextProtocol.AspNetCore/2.3.1)
