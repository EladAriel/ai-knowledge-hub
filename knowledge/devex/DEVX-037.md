# DEVX-037: FastMCP Generative UI sandbox escape (CVE-2026-120338, CVSS 10.0)

## Summary

prefab-ui 0.14.0–0.20.2 ran its Deno sandbox with full read/write/network, so any client calling generate_prefab_ui (or a prompt injection writing its code argument) can read/write files as the server user. Fixed in 0.21.0; advisory not public, so Dependabot won't flag it.

## Details

Affected: only FastMCP servers using add_provider(GenerativeUI()); fastmcp[apps] still allows prefab-ui>=0.18.0 so lockfiles can stay vulnerable. PoC (agent's own): pip show prefab-ui | grep -i ^version ; grep -rn "GenerativeUI" --include=*.py . ; uv add 'prefab-ui>=0.21.0'. Success: no deployed FastMCP server below 0.21.0, every GenerativeUI server requires auth. Stage Adopt, feasibility High. Seen in 4 sources, expires 2027-01-31.

## Sources

- [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-120338)
- [fix PR #538](https://github.com/PrefectHQ/prefab/pull/538)
- [v0.21.0](https://github.com/PrefectHQ/prefab/releases/tag/v0.21.0)
- [FastMCP Generative UI docs](https://gofastmcp.com/apps/generative)
