# GPG

## SSH integration

**Issue**

When trying to push to a Git repository using an SSH key managed by GPG, you may see:

```
$ git push
sign_and_send_pubkey: signing failed for ED25519 "(none)" from agent: agent refused operation
```

This happens because the gpg-agent (which can act as an SSH agent) doesn’t know
which terminal to use for prompting for a passphrase. SSH doesn’t automatically
communicate terminal information to GPG.

**Solution (Fish Shell)**

```
$ cat .ssh/config 
Match host * exec "set -x GPG_TTY (tty <&2) && gpg-connect-agent updatestartuptty /bye"
```
