# DEVX-097: Upgrade Obot MCP gateway to 0.27.0 (two high CVEs: token theft, SSRF)

## Summary

Obot MCP gateway has two high CVEs: CVE-2026-130766 (token theft) and CVE-2026-130764 (SSRF). Fixed in 0.27.0, so upgrade.

## Details

- Upgrade Obot to 0.27.0.
- Advisories: CVE-2026-130766 (GHSA-vrfj-v4c4-f8qr), CVE-2026-130764 (GHSA-x4wv-wh23-vxjx).
- Reported Nov 19.

## Sources

- [CVE-2026-130766](https://github.com/advisories/GHSA-vrfj-v4c4-f8qr)
- [CVE-2026-130764](https://github.com/advisories/GHSA-x4wv-wh23-vxjx)
