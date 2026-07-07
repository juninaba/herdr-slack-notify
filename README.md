# Herdr Slack Notify

Herdr Slack Notify sends a Slack message when an agent reaches `done` or `blocked` status.

Requires Node.js 18+. Zero npm dependencies.

## Setup

Create a Slack incoming webhook and copy the webhook URL:

<https://api.slack.com/messaging/webhooks>

Install locally while developing:

```sh
herdr plugin link .
```

Or install from GitHub once published:

```sh
herdr plugin install juninaba/herdr-slack-notify
```

Create the plugin config:

```sh
CONFIG_DIR="$(herdr plugin config-dir agent-slack-notify)"
mkdir -p "$CONFIG_DIR"
cp .env.example "$CONFIG_DIR/.env"
```

Set `SLACK_WEBHOOK_URL` in `$CONFIG_DIR/.env`:

```env
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/XXX/YYY/ZZZ
```

Confirm the actions are visible:

```sh
herdr plugin action list --plugin agent-slack-notify
```

Toggle notifications:

```sh
herdr plugin action invoke toggle --plugin agent-slack-notify
```

## Keybinding

Bind the toggle action from `~/.config/herdr/config.toml`:

```toml
[[keys.command]]
key = "prefix+s"
type = "plugin_action"
command = "agent-slack-notify.toggle"
description = "toggle Slack notify"
```

Reload Herdr after changing the config:

```sh
herdr server reload-config
```
