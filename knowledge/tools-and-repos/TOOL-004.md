# TOOL-004: protect-mcp starter policy hook

## Summary

Built-in starter policy blocks force-pushing to main, 'rm -rf /', reading secrets, and 'curl | sh', with signed receipts.

## Details

With 'onFailure: block', it also blocks if the check itself fails. ….

## Sources

- [protect-mcp](https://www.npmjs.com/package/protect-mcp)
