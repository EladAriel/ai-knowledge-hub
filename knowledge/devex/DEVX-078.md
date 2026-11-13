# DEVX-078: Phone ping when Claude Code needs you (Notification hook via ntfy)

## Summary

Ready-to-use mod: a Notification hook that sends a push through ntfy, so you stop babysitting the terminal. ~3 min. Keep the message generic: public ntfy.sh topics are readable by anyone who guesses the name, so self-host it for work.

## Details

In `~/.claude/settings.json`: a Notification command hook running `curl -s -d 'Claude Code needs input' https://ntfy.sh/\<your-random-topic>` (full snippet below). Credit: @fellyroy on X.

## Content

- [Phone ping when Claude needs you](https://x.com/fellyroy/status/2120215991825113135): a Notification hook that sends a push through ntfy, so you stop babysitting the terminal. ~3 min. Keep the message generic: public ntfy.sh topics are readable by anyone who guesses the name, so self-host it for work. In `~/.claude/settings.json`:
```json
{ "hooks": { "Notification": [ { "hooks": [ { "type": "command",
  "command": "curl -s -d 'Claude Code needs input' https://ntfy.sh/<your-random-topic>" } ] } ] } }
```

Credit: the ntfy hook is from @fellyroy on X.

## Sources

- [@fellyroy on X](https://x.com/fellyroy/status/2120215991825113135)
