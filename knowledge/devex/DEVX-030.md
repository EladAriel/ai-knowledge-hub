# DEVX-030: Cursor install cooldown and extension allowlist

## Summary

After the backdoored Claude Code extension incident: a team-level install cooldown plus an allowlist that pins exact extension versions.

## Content

### Cursor install cooldown and extension allowlist — Enterprise feasibility: High | Stage: Adopt
- **What changed:** Microsoft's write-up recommends both controls after the backdoor incident. A team-level cooldown overrides each user's `extensions.installCooldownHours`. `extensions.allowed`, or `AllowedExtensions` pushed by MDM (device management), can pin exact extension versions.
- **Effort:** about 30 min.
- **PoC:** In Team settings, open Security & automation and set Marketplace Install Cooldown to 72 hours (the value is my choice). Then add an allowlist:
```json
{ "anysphere": true, "github": true, "dbaeumer.vscode-eslint": ["3.0.0"] }
```
- **Success metric:** no hosts with the `svc-telemetry` key, and the cooldown plus allowlist deployed on every managed Cursor client.
- **Sources:** [Cursor extensions help](https://cursor.com/help/customization/extensions), [allowed extensions docs](https://cursor.com/docs/enterprise/identity-and-access-management#allowed-extensions). Seen in 7 sources. Expires Jan 30, 2027.

## Sources

- [Cursor extensions help](https://cursor.com/help/customization/extensions)
- [allowed extensions docs](https://cursor.com/docs/enterprise/identity-and-access-management#allowed-extensions)
