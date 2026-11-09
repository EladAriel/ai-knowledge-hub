# DEVX-031: Upgrade the open npm package to 11+ (CVE-2026-119025)

## Summary

On Windows/WSL a crafted URL passed to open runs PowerShell code (e.g. a malicious MCP server's OAuth endpoint); root cause of earlier Inspector and opencode RCEs. Dependabot won't flag it.

## Details

Run npm ls open --all, then force the fix in package.json: { "overrides": { "open": "^11.0.4" } }. Only breaking change in 11 is Node 20+. Success: no copies of open below 11 in internal tools that handle remote URLs. Stage Adopt.

## Sources

- [VulnCheck advisory](https://www.vulncheck.com/advisories/open-7.2.0-before-11.0.0-os-command-injection-via-powershell-on-windows)
- [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-119025)
- [open v11.0.0](https://github.com/sindresorhus/open/releases/tag/v11.0.0)
