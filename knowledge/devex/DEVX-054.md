# DEVX-054: Upgrade MCP Inspector to 2.14.0 (or 1.0.4 on v1): three medium security advisories fixed

## Summary

MCP Inspector 2.14.0 (npm latest) and deprecated 1.0.4 (v1-latest) fix three medium advisories: MCP App sandbox-frame escape (connectDomains was not an egress boundary), unvalidated server.json import and non-http(s) URL elicitations, and an outputSchema.pattern ReDoS. Upgrade before connecting untrusted servers or reviewing MCP Apps.

## Details

Released Nov 5 around 01:55–02:17 Israel time. GHSA-h9j8-vj8g-v3gg (CVSS 6.1): an MCP App can navigate its sandbox frame away while the proxy still relays with targetOrigin '*', so the app's connectDomains CSP was not an egress boundary (v2 only, >=2.0.0 \<=2.13.0). GHSA-rwv7-mh2c-ff2p: server.json import did not validate runtimeArguments / identifier / environment variables, and URL elicitations accepted non-http(s) schemes; import now shows the exact command before save. GHSA-2fw8-7jmw-r937 (CVSS 6.5): a malicious tool outputSchema.pattern can ReDoS-stall the UI; v2 uses a bounded linear-time matcher, v1.0.4 strips patterns. Node engine floor is now ^22.23.4 || ^24.22.1 || >=26.12.1 (EBADENGINE is advisory only). Who is affected: anyone who imports server.json, opens URL elicitations, calls tools on third-party servers, or renders MCP Apps; CLI/TUI users on \<=2.13.0 are still exposed to the ReDoS and import issues. How: always run via @latest / @v1-latest so a cached 2.13.0 / 1.0.3 is not reused. PoC: npm view @modelcontextprotocol/inspector dist-tags (expect latest=2.14.0, v1-latest=1.0.4); npx @modelcontextprotocol/inspector@latest. Success metric: fleet Inspector invocations resolve to >=2.14.0 (or >=1.0.4 on v1). Org challenge: teams that vendor a pinned Inspector Docker image or lockfile need an explicit bump. Enterprise feasibility High, stage Adopt, seen in 5 sources.

## Content

**[MCP Inspector 2.14.0 (and deprecated v1.0.4) fix three medium security advisories; npm latest is now 2.14.0 and v1-latest is 1.0.4](https://github.com/modelcontextprotocol/inspector/releases/tag/2.14.0)**
- **summary:** GitHub release 2.14.0 published Nov 4 at 23:55Z (01:55 Israel time, Nov 5); npm @modelcontextprotocol/inspector@2.14.0 landed Nov 5 at 00:17Z (02:17 Israel time). v1.0.4 published Nov 4 at 23:28Z / npm 23:34Z. Three privately reported medium advisories: (1) GHSA-h9j8-vj8g-v3gg (CVSS 6.1) — an MCP App can navigate its sandbox frame away from the host-loaded document; the proxy kept relaying with targetOrigin '*', so the app's connectDomains CSP was not an egress boundary. Fixed only in 2.14.0 (v2 >=2.0.0 <=2.13.0). (2) GHSA-rwv7-mh2c-ff2p — unvalidated runtimeArguments/identifier/environmentVariables on server.json import, plus URL elicitations that accepted non-http(s) schemes; import now shows the exact command before save and refuses unsafe tokens / non-http(s) URLs. Fixed in 2.14.0. (3) GHSA-2fw8-7jmw-r937 (CVSS 6.5) — a malicious tool outputSchema.pattern can ReDoS-stall the UI; v2 uses a bounded linear-time matcher, and deprecated v1.0.4 strips patterns entirely. Also: Node engine floor raised to ^22.23.4 || ^24.22.1 || >=26.12.1 (Oct 2026 Node security releases); npm prints EBADENGINE on older Node but the field is advisory. Upgrade: npx @modelcontextprotocol/inspector@latest (or @v1-latest on the deprecated line).
- **verified:** true

## Breaking-change alerts
- **MCP Inspector 2.14.0 (npm `latest`) and deprecated 1.0.4 (`v1-latest`) fix three medium advisories.** Released Nov 5 around 01:55–02:17 Israel time ([2.14.0](https://github.com/modelcontextprotocol/inspector/releases/tag/2.14.0)). [GHSA-h9j8-vj8g-v3gg](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-h9j8-vj8g-v3gg) (CVSS 6.1): an MCP App can navigate its sandbox frame away while the proxy still relays with `targetOrigin '*'`, so `connectDomains` was not an egress boundary (v2 only, `>=2.0.0 <=2.13.0`). [GHSA-rwv7-mh2c-ff2p](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-rwv7-mh2c-ff2p): `server.json` import did not validate `runtimeArguments` / identifier / env vars, and URL elicitations accepted non-http(s) schemes; import now shows the exact command before save. [GHSA-2fw8-7jmw-r937](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-2fw8-7jmw-r937) (CVSS 6.5): a malicious `outputSchema.pattern` can ReDoS-stall the UI; v2 uses a bounded matcher, v1.0.4 strips patterns. Node engine floor is now `^22.23.4 || ^24.22.1 || >=26.12.1` (advisory `EBADENGINE` only). Upgrade with `npx @modelcontextprotocol/inspector@latest` (or `@v1-latest`).

**[Upgrade MCP Inspector to 2.14.0 (or 1.0.4 on the deprecated v1 line) before connecting untrusted servers or reviewing MCP Apps](https://github.com/modelcontextprotocol/inspector/releases/tag/2.14.0)**
- **urls_extra:** ["https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-h9j8-vj8g-v3gg", "https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-rwv7-mh2c-ff2p", "https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-2fw8-7jmw-r937", "https://forkast.news/mcp-inspector-2-14-0-fixes-three-privately-reported-vulnerabilities-and-changes-developer-facing-behavior/"]
- **what_changed:** See breaking alert. Anyone who uses Inspector to import server.json, open URL elicitations, call tools on third-party servers, or render MCP Apps in the web client's Apps tab is in the affected set for at least one of the three GHSAs. CLI/TUI users who never open Apps are still exposed to the ReDoS and import issues on v2 <=2.13.0.
- **how_it_works:** Pin or always run via npx @latest / @v1-latest so local caches of 2.13.0 / 1.0.3 are not reused. After upgrade, server.json import shows the command before save; over-limit schema patterns are reported unverified (v2) or stripped (v1).
- **enterprise_feasibility:** High
- **stage:** Adopt
- **effort_minutes:** 10
- **poc_snippet:** npm view @modelcontextprotocol/inspector dist-tags   # expect latest=2.14.0, v1-latest=1.0.4
npx @modelcontextprotocol/inspector@latest            # or @v1-latest on the deprecated line
# optional: pin Node to the new floor ^22.23.4 || ^24.22.1 || >=26.12.1
- **success_metric:** Fleet Inspector invocations resolve to >=2.14.0 (or >=1.0.4 on v1); no developer machines left on 2.13.0/1.0.3.
- **org_challenge_if_relevant:** Teams that vendor a pinned Inspector Docker image or lockfile need an explicit bump; EBADENGINE on older Node is advisory only.
- **project_health_if_relevant:** Official MCP org release plus three published repo advisories; secondary write-up on Forkast.
- **source_count:** 5
- **benefit_to_effort:** Very high
- **why_enterprise_simple:** One npx channel bump closes three medium issues that hit the exact tool used to vet third-party MCP servers.

## Sources

- [Inspector 2.14.0 release](https://github.com/modelcontextprotocol/inspector/releases/tag/2.14.0)
- [GHSA-h9j8](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-h9j8-vj8g-v3gg)
- [GHSA-rwv7](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-rwv7-mh2c-ff2p)
- [GHSA-2fw8](https://github.com/modelcontextprotocol/inspector/security/advisories/GHSA-2fw8-7jmw-r937)
- [Forkast write-up](https://forkast.news/mcp-inspector-2-14-0-fixes-three-privately-reported-vulnerabilities-and-changes-developer-facing-behavior)