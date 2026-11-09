# DEVX-037: FastMCP Generative UI sandbox escape (CVE-2026-120338, CVSS 10.0)

## Summary

prefab-ui 0.14.0–0.20.2 ran its Deno sandbox with full read/write/network, so any client calling generate_prefab_ui (or a prompt injection writing its code argument) can read/write files as the server user. Fixed in 0.21.0; advisory not public, so Dependabot won't flag it.

## Content

### FastMCP Generative UI sandbox escape (CVE-2026-120338, CVSS 10.0) — Enterprise feasibility: High | Stage: Adopt
- **What changed:** `prefab-ui` 0.14.0 through 0.20.2 ran its Deno sandbox with full read, write and network access. So any client that can call `generate_prefab_ui`, or a prompt injection that writes its `code` argument, can read and write files as the server user and stay on the machine. The fix is in 0.21.0. The GitHub advisory isn't public yet, so Dependabot won't flag old lockfiles.
- **Who's affected:** only FastMCP servers that call `add_provider(GenerativeUI())`. `fastmcp[apps]` still allows `prefab-ui>=0.18.0`, so an existing lockfile can stay on a vulnerable version.
- **Effort:** about 15 min.
- **PoC:** these commands are my own, not from the advisory.
```bash
pip show prefab-ui | grep -i ^version     # vulnerable: 0.14.0–0.20.2
grep -rn "GenerativeUI" --include=*.py .
uv add 'prefab-ui>=0.21.0'                # or: pip install -U 'prefab-ui>=0.21.0'
```
- **Success metric:** no deployed FastMCP server has `prefab-ui` below 0.21.0, and every server with GenerativeUI requires auth.
- **Sources:** [NVD entry](https://nvd.nist.gov/vuln/detail/CVE-2026-120338), [fix PR #538](https://github.com/PrefectHQ/prefab/pull/538), [v0.21.0 release](https://github.com/PrefectHQ/prefab/releases/tag/v0.21.0), [FastMCP Generative UI docs](https://gofastmcp.com/apps/generative). Seen in 4 sources. Expires Jan 31, 2027.

## Sources

- [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-120338)
- [fix PR #538](https://github.com/PrefectHQ/prefab/pull/538)
- [v0.21.0](https://github.com/PrefectHQ/prefab/releases/tag/v0.21.0)
- [FastMCP Generative UI docs](https://gofastmcp.com/apps/generative)
