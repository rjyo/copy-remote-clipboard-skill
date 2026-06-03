---
name: copy-remote-clipboard
description: Copy text to the user's remote or terminal clipboard with OSC52. Use when the user says "copy this to my remote clipboard", "copy this to my terminal clipboard", or asks Codex to send text to their clipboard from the terminal.
---

# Copy Remote Clipboard

## Prerequisites

- `base64` exists on PATH.
- The terminal allows OSC52 clipboard writes.
- In tmux, `set -g set-clipboard on` is enabled.

## Workflow

Copy only text the user explicitly asked to copy.

```sh
tty_target="$(tmux display-message -p '#{client_tty}')"
payload="$(printf %s 'TEXT_TO_COPY' | base64 | tr -d '\n')"
printf '\033]52;c;%s\a' "$payload" > "$tty_target"
```

If tmux is unavailable, try:

```sh
payload="$(printf %s 'TEXT_TO_COPY' | base64 | tr -d '\n')"
printf '\033]52;c;%s\a' "$payload" > /dev/tty
```

If there is no real TTY, tell the user Codex cannot deliver OSC52 from captured stdout.
