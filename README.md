# Copy Remote Clipboard Skill

A small Codex skill for copying text to a remote or terminal clipboard with OSC52.

## Install

Copy or symlink the skill folder into your Codex skills directory:

```sh
mkdir -p ~/.codex/skills
cp -R copy-remote-clipboard ~/.codex/skills/
```

## Prerequisites

- `base64` is available on PATH.
- Your terminal emulator allows OSC52 clipboard writes.
- If you use tmux, enable clipboard passthrough:

```tmux
set -g set-clipboard on
```

Reload tmux after changing the config:

```sh
tmux source-file ~/.tmux.conf
```

## Example

Ask Codex:

```text
Tell me a joke and copy it to my remote clipboard.
```

The skill will generate the text and send it to the terminal clipboard through OSC52.
