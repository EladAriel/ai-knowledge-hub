# DEVX-030: Cursor install cooldown and extension allowlist

## Summary

After the backdoored Claude Code extension incident: a team-level install cooldown plus an allowlist that pins exact extension versions.

## Details

Team cooldown overrides each user's extensions.installCooldownHours; extensions.allowed (or AllowedExtensions via MDM) can pin versions.

## Sources

- [Cursor extensions help](https://cursor.com/help/customization/extensions)
- [allowed extensions docs](https://cursor.com/docs/enterprise/identity-and-access-management#allowed-extensions)
