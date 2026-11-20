# DEVX-092: Windows 11 reports which coding agents you use: set diagnostic data to Required

## Summary

A reverse-engineering write-up (718 points on HN) found Windows 11's MissionControlAggregator recording whether claude.exe, codex.exe, cursor.exe, copilot.exe and other dev tools were used. It uploads that through optional diagnostic data, which was on by default in the author's clean US install. The event is marked optional, so the Required level shouldn't send it. Enterprise feasibility: High. Stage: Adopt. Effort: about 5 minutes per policy.

## Details

Set it with GPO (Computer Configuration > Administrative Templates > Windows Components > Data Collection and Preview Builds > Allow diagnostic data) or with MDM `System/AllowTelemetry`. Practical PoC (admin prompt, 1 = Required):
```bat
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection" /v AllowTelemetry /t REG_DWORD /d 1 /f
```
Success metric: `reg query` returns `0x1` on every developer machine. Seen in 3 sources. Expires Feb 16, 2027.

## Sources

- [xusheng.dev write-up](https://xusheng.dev/posts/windows-coding-agent-telemetry/)
- [HN thread](https://news.ycombinator.com/item?id=50524736)
- [Microsoft: configure diagnostic data](https://learn.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization)
