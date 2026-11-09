# DEVX-028: Cursor cloud agents to internal MCP via Tailscale

## Summary

A new Cursor docs page shows Rollouts joining your tailnet as an ephemeral, tagged device.

## Content

### 4. Cursor cloud agents to internal MCP via Tailscale — Enterprise feasibility: Medium | Stage: Assess
- **What changed:** A new [Cursor docs page](https://cursor.com/docs/integrations/tailscale) shows Rollouts joining your tailnet as an ephemeral, tagged device with a 10-minute single-use key. That lets cloud agents reach an internal https MCP server without exposing it publicly. It's a beta that sales has to turn on, and the only source so far is the docs page.
- **Effort:** ~45 min.
- **PoC** (tailnet policy):
```json
{ "tagOwners": { "tag:cursor": ["autogroup:admin"], "tag:mcp": ["autogroup:admin"] },
  "acls": [ { "action": "accept", "src": ["tag:cursor"], "dst": ["tag:mcp:443"] } ] }
```

## Sources

- [Cursor docs page](https://cursor.com/docs/integrations/tailscale)
