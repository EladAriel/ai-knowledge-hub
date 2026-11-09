# TOOL-005: Turn-inspector

## Summary

Adds a '/turns' view of what fills each request's context window, which helps find token drains (~5 min).

## Details

Credit: davila7/claude-code-templates. npx claude-code-templates@latest --mod ui/turn-inspector, then in a session: /turns

## Content

**[Turn-inspector](https://github.com/davila7/claude-code-templates/pull/1167)** adds a `/turns` view that shows what fills each request's context window, which helps you find token drains (~5 min):
```bash
npx claude-code-templates@latest --mod ui/turn-inspector
```

## Sources

- [Turn-inspector](https://github.com/davila7/claude-code-templates/pull/1167)