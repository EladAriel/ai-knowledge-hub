# DEVX-071: Keep your SSH agent out of agent sessions (unset SSH_AUTH_SOCK)

## Summary

Any coding agent's shell inherits SSH_AUTH_SOCK, so it can push to your private repos with your SSH key. Start agents without that variable (HN flagged ChatGPT Desktop forwarding the SSH agent to remote machines). Feasibility High, stage Adopt, ~5 min.

## Details

PoC: `alias claude='env -u SSH_AUTH_SOCK claude'` (and `alias cursor-agent='env -u SSH_AUTH_SOCK cursor-agent'`) in ~/.zshrc; inside a session `ssh-add -l` should print 'Could not open a connection to your authentication agent'.
Top commenters suggest keys that need a fingerprint on every use; newer macOS can create Secure Enclave SSH keys that do this.
Success metric: zero agent-initiated pushes over SSH; pushes happen from your own terminal or a scoped HTTPS token. Seen in 2 sources. Expires Feb 8, 2027.

## Content

### 2. Keep your SSH agent out of agent sessions — Enterprise feasibility: High | Stage: Adopt
- What changes: an agent can't push to your private repos with your SSH key unless you're there to approve it.
- How it works: HN (208 points) flagged that ChatGPT Desktop forwards your SSH agent to remote machines. The same exposure exists locally, because any coding agent's shell inherits `SSH_AUTH_SOCK`, the socket your SSH agent listens on. Start agents without that variable. Top commenters suggest keys that need a fingerprint on every use; newer macOS can create Secure Enclave SSH keys that do this.
- Effort: ~5 min.
- PoC: `alias claude='env -u SSH_AUTH_SOCK claude'` in `~/.zshrc`, then inside a session run `ssh-add -l`. You should get "Could not open a connection to your authentication agent".
- Success metric: zero agent-initiated pushes over SSH. Pushes happen from your own terminal or a scoped HTTPS token.
- Sources: [HN thread](https://news.ycombinator.com/item?id=50422628), [Secure Enclave SSH keys gist](https://gist.github.com/arianvp/5f59f1783e3eaf1a2d4cd8e952bb4acf) | seen in 2 sources | expires Feb 8, 2027

- [No-SSH-agent launcher](https://news.ycombinator.com/item?id=50422628): starts Claude Code and Cursor's CLI agent without your SSH agent. ~1 min. Add to `~/.zshrc`:
```bash
alias claude='env -u SSH_AUTH_SOCK claude'
alias cursor-agent='env -u SSH_AUTH_SOCK cursor-agent'
```

## Sources

- [HN thread](https://news.ycombinator.com/item?id=50422628)
- [Secure Enclave SSH keys gist](https://gist.github.com/arianvp/5f59f1783e3eaf1a2d4cd8e952bb4acf)
