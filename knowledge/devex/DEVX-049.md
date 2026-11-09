# DEVX-049: MCP HTTP session hijack: C# SDK (GHSA-x863-g495-4cjc) and SurrealDB MCP (CVE-2026-121419), plus a cross-user replay test

## Summary

Both bound a session to an identity several users share (null claim, or the access-method name), so a user holding another's Mcp-Session-Id could take over. Upgrade ModelContextProtocol.AspNetCore to >= 2.3.1 / 1.4.2 and SurrealDB to >= 3.3.0, and test every HTTP MCP server by replaying user A's session with user B's token (expect 403).

## Details

C# SDK: high, CVSS 7.5, published Nov 3; affected >= 0.1.0-preview.9 \< 1.4.2 and >= 2.0.0-preview.1 \< 2.3.1. Fix fails closed: principals without NameIdentifier/sub/UPN get 403 on stateful sessions; add an IClaimsTransformation that maps your own ID claim to NameIdentifier (from the SDK docs). On 1.4.2 OAuth discovery validates PKCE and metadata issuer; metadata-free 2025-03-26 servers must advertise S256 or opt in to AllowLegacyOAuthMetadataFallback. SurrealDB 3.1.0 to \< 3.3.0: BoundSubject used the access-method name for JWT/Bearer DEFINE ACCESS, letting a viewer act with an editor's roles (CVSS 4.0 8.6). Instatic CVE-2026-121458 is a third same-day case of MCP path having weaker authz than the API. PoC: dotnet list package | grep -i ModelContextProtocol.AspNetCore; surreal version; curl -s -o /dev/null -w '%{http_code}' -X POST $MCP_URL -H "Authorization: Bearer $TOKEN_B" -H "Mcp-Session-Id: $SESSION_A" -H 'Content-Type: application/json' -H 'Accept: application/json, text/event-stream' -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'. Success metric: all C# MCP servers >= 2.3.1/1.4.2, SurrealDB >= 3.3.0, cross-user replay returns 403 everywhere. Org challenge: API-key or cert auth without those claims will start returning 403 until the transformation is added, so test in staging. Feasibility High, stage Adopt.

## Content

**[Two MCP HTTP session-hijack bugs disclosed on the same day: MCP C# SDK (GHSA-x863-g495-4cjc, CVSS 7.5) and SurrealDB MCP (CVE-2026-121419, CVSS 4.0 8.6). Both bound a session to an identity that several users share](https://nvd.nist.gov/vuln/detail/CVE-2026-121419)**
- **urls_extra:** ["https://github.com/surrealdb/surrealdb/security/advisories/GHSA-pgh9-49q4-hqcx", "https://www.vulncheck.com/advisories/surrealdb-3.1.0-before-3.3.0-mcp-session-hijack-via-boundsubject-collision", "https://github.com/modelcontextprotocol/csharp-sdk/security/advisories/GHSA-x863-g495-4cjc", "https://www.nuget.org/packages/ModelContextProtocol.AspNetCore/2.3.1"]
- **what_changed:** SurrealDB 3.1.0 to before 3.3.0: the MCP `BoundSubject` fingerprint used the access-method name (for example 'api') rather than the user, for JWT/Bearer `DEFINE ACCESS`. Any low-privilege user of that method who had a victim's `mcp-session-id` could run MCP tools with the victim's roles. The advisory reproduces a viewer writing to a record only an editor may change. NVD published it Nov 3 at 15:17Z (17:17 Israel time); the repo advisory dates from Oct 19, and the fix is in 3.3.0 (current v4.0.0 shipped Nov 3). The C# SDK bug is the same class. Instatic CVE-2026-121458, where MCP read tools skip the HTTP API's object-level checks, is a third same-day example of 'the MCP path has weaker authz than the API'.
- **how_it_works:** In both cases the session-to-user check compared something that's identical across users (null, or the access-method name). The fix is to upgrade. A quick self-test for any in-house MCP server: start a session as user A, then send A's Mcp-Session-Id with user B's token. Anything other than 403 is a bug.
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 30
- **poc_snippet:** # upgrade (my composition)
dotnet list package | grep -i ModelContextProtocol.AspNetCore   # need >= 2.3.1 (or 1.4.2 on 1.x)
surreal version                                                 # need >= 3.3.0

// C# servers whose auth has no NameIdentifier/sub/UPN claim: add the SDK's documented mapping (from docs/concepts/stateless/stateless.md, v2.3.1)
builder.Services.AddTransient<IClaimsTransformation, McpUserIdClaimsTransformation>();
public sealed class McpUserIdClaimsTransformation : IClaimsTransformation
{
    public Task<ClaimsPrincipal> TransformAsync(ClaimsPrincipal principal)
    {
        if (principal.Identity is ClaimsIdentity identity &&
            identity.FindFirst(ClaimTypes.NameIdentifier) is null &&
            identity.FindFirst("custom-user-id") is { } userId)
        {
            identity.AddClaim(new Claim(
                ClaimTypes.NameIdentifier, userId.Value, userId.ValueType, userId.Issuer));
        }
        return Task.FromResult(principal);
    }
}

# cross-user session test for any HTTP MCP server: replay A's session with B's token, expect 403
curl -s -o /dev/null -w '%{http_code}\n' -X POST $MCP_URL -H "Authorization: Bearer $TOKEN_B" -H "Mcp-Session-Id: $SESSION_A" -H 'Content-Type: application/json' -H 'Accept: application/json, text/event-stream' -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
- **success_metric:** All C# MCP servers on >= 2.3.1/1.4.2 and SurrealDB on >= 3.3.0. The cross-user replay returns 403 on every internal HTTP MCP server.
- **org_challenge_if_relevant:** The C# fix fails closed. Servers using API-key or certificate auth without those claims will start returning 403 until the claims transformation is added, so test in staging first.
- **project_health_if_relevant:** C# SDK: official MCP org, patched releases on NuGet, global GHSA entry not yet live (404). SurrealDB: vendor advisory, CVE through VulnCheck.
- **source_count:** 4
- **benefit_to_effort:** High (audience: teams running HTTP MCP servers on .NET or SurrealDB)
- **why_enterprise_simple:** A package bump plus one curl test covers a whole class of multi-user MCP bugs.

### 3. Test your HTTP MCP servers for cross-user session takeover — Enterprise feasibility: High | Stage: Adopt
- **What changed:** two bugs of the same kind came out the same day: the C# SDK advisory above, and SurrealDB [CVE-2026-121419](https://nvd.nist.gov/vuln/detail/CVE-2026-121419) (versions 3.1.0 up to 3.3.0, CVSS 4.0 score 8.6, fixed in 3.3.0). In both, a session was tied to an identity that several users share.
- **Effort:** ~30 min
- **PoC:** upgrade first (`dotnet list package | grep -i ModelContextProtocol.AspNetCore` should show 2.3.1 or later, and `surreal version` should show 3.3.0 or later). Then replay user A's session with user B's token and expect a 403:
```bash
curl -s -o /dev/null -w '%{http_code}\n' -X POST $MCP_URL -H "Authorization: Bearer $TOKEN_B" -H "Mcp-Session-Id: $SESSION_A" -H 'Content-Type: application/json' -H 'Accept: application/json, text/event-stream' -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```
- **Caveat:** C# servers that use API-key or certificate auth without those claims will start returning 403. The SDK documents an `IClaimsTransformation` that maps your own user-ID claim to NameIdentifier; test it in staging first.
- **Success metric:** the cross-user replay returns 403 on every internal MCP server.
- **Sources:** [SurrealDB advisory](https://github.com/surrealdb/surrealdb/security/advisories/GHSA-pgh9-49q4-hqcx), [C# SDK advisory](https://github.com/modelcontextprotocol/csharp-sdk/security/advisories/GHSA-x863-g495-4cjc), [VulnCheck](https://www.vulncheck.com/advisories/surrealdb-3.1.0-before-3.3.0-mcp-session-hijack-via-boundsubject-collision), [NuGet 2.3.1](https://www.nuget.org/packages/ModelContextProtocol.AspNetCore/2.3.1) | seen in 4 sources

## Sources

- [GHSA-x863-g495-4cjc](https://github.com/modelcontextprotocol/csharp-sdk/security/advisories/GHSA-x863-g495-4cjc)
- [CVE-2026-121419](https://nvd.nist.gov/vuln/detail/CVE-2026-121419)
- [SurrealDB advisory](https://github.com/surrealdb/surrealdb/security/advisories/GHSA-pgh9-49q4-hqcx)
- [NuGet 2.3.1](https://www.nuget.org/packages/ModelContextProtocol.AspNetCore/2.3.1)
- [VulnCheck](https://www.vulncheck.com/advisories/surrealdb-3.1.0-before-3.3.0-mcp-session-hijack-via-boundsubject-collision)