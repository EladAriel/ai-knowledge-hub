# DEVX-068: sandbox-mcp: throwaway network-off Windows 11 Sandbox for agent app tests

## Summary

An sbx CLI plus optional MCP adapter on Windows Sandbox: an agent installs and clicks through your Windows app on a fresh, network-off guest, keeps screenshots and exit codes as evidence, then throws the machine away. Only for Windows desktop apps on Windows Pro/Enterprise. Feasibility Medium, stage Assess, ~20 min.

## Details

Installs a runtime only with --provision auto. PoC: sbx deps app.exe, then sbx run app.exe on a fresh guest. Setup: enable Windows Sandbox and download the portable v1.2.0 release. Skip for pure web work.
Project health: Scott Hanselman, MIT, created Nov 6, about 345 stars, single maintainer. Expires Feb 7, 2027.

## Content

### sandbox-mcp: throwaway Windows 11 for agent app tests — Enterprise feasibility: Medium | Stage: Assess
- What changes: an agent can install and click through your Windows app on a fresh, network-off Windows Sandbox and keep screenshots and exit codes as evidence, then throw the machine away. That catches "works on my machine" dependency bugs.
- How it works: an `sbx` CLI plus an optional MCP adapter on top of Windows Sandbox. It only installs a runtime when you pass `--provision auto`. It's only useful if you ship Windows desktop apps (WPF, WinUI, Win32) and run Windows Pro or Enterprise; skip it for pure web work.
- Effort: ~20 min (enable Windows Sandbox and download the portable v1.2.0 release).
- PoC: `sbx deps app.exe`, then `sbx run app.exe` on a fresh guest.
- Project health: Scott Hanselman, MIT, created Nov 6, about 345 stars, single maintainer.
- Sources: [shanselman/sandbox-mcp](https://github.com/shanselman/sandbox-mcp) | seen in 1 source | expires Feb 7, 2027

## Sources

- [shanselman/sandbox-mcp](https://github.com/shanselman/sandbox-mcp)
