# DEVX-031: Upgrade the open npm package to 11+ (CVE-2026-119025)

## Summary

On Windows/WSL a crafted URL passed to open() runs PowerShell code (e.g. a malicious MCP server's OAuth endpoint); root cause of earlier Inspector and opencode RCEs. Dependabot won't flag it.

## Details

Run npm ls open --all, then force the fix in package.json: { "overrides": { "open": "^11.0.4" } }. Only breaking change in 11 is Node 20+. Success: no copies of open below 11 in internal tools that handle remote URLs. Stage Adopt.

## Content

### `open` npm package below 11.0.0 (CVE-2026-119025) — Enterprise feasibility: High | Stage: Adopt
- **What changed:** On Windows and WSL, a crafted URL passed to `open()` runs PowerShell code. One example is a malicious MCP server's OAuth endpoint. This is the root cause behind the Inspector and opencode RCEs (remote code execution bugs) reported earlier. The GitHub advisory lists no package, so Dependabot won't flag it.
- **Effort:** about 30 min.
- **PoC:** Run `npm ls open --all`, then force the fixed version in `package.json`. The only breaking change in 11 is that it needs Node 20+.
```json
{ "overrides": { "open": "^11.0.4" } }
```
- **Success metric:** no copies of `open` below 11 in internal tools that handle remote URLs.
- **Sources:** [VulnCheck advisory](https://www.vulncheck.com/advisories/open-7.2.0-before-11.0.0-os-command-injection-via-powershell-on-windows), [NVD entry](https://nvd.nist.gov/vuln/detail/CVE-2026-119025), [open v11.0.0 release](https://github.com/sindresorhus/open/releases/tag/v11.0.0). Seen in 4 sources. Expires Jan 30, 2027.

## Sources

- [VulnCheck advisory](https://www.vulncheck.com/advisories/open-7.2.0-before-11.0.0-os-command-injection-via-powershell-on-windows)
- [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-119025)
- [open v11.0.0](https://github.com/sindresorhus/open/releases/tag/v11.0.0)