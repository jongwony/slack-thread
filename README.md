# slack-thread

Unix-style tool to fetch Slack thread conversations for piping to other tools.

## Installation

```bash
# One-liner (recommended)
curl -fsSL https://raw.githubusercontent.com/jongwony/slack-thread/main/install | bash

# Or clone and symlink
git clone https://github.com/jongwony/slack-thread
ln -s $(pwd)/slack-thread/slack-thread /usr/local/bin/slack-thread
```

Advanced install options:

```bash
# Choose install directory
curl -fsSL https://raw.githubusercontent.com/jongwony/slack-thread/main/install | bash -s -- --to "$HOME/.local/bin"

# Force overwrite existing binary
curl -fsSL https://raw.githubusercontent.com/jongwony/slack-thread/main/install | bash -s -- --force

# Also install 'uv' automatically if missing
curl -fsSL https://raw.githubusercontent.com/jongwony/slack-thread/main/install | bash -s -- --install-uv
```

## Setup

### Option 1: User Token (Recommended for Personal Use)
Access only threads you can see:

1. Create app at https://api.slack.com/apps
2. Go to **OAuth & Permissions** → **User Token Scopes**
3. Add scopes: `channels:history`, `groups:history`, `im:history`, `mpim:history`, `users:read`
4. Install app to workspace
5. Copy **User OAuth Token** (starts with `xoxp-`)

```bash
export SLACK_USER_TOKEN='xoxp-your-user-token'
```

### Option 2: Bot Token (For Servers/CI)
Access all channels where bot is added:

1. Create app at https://api.slack.com/apps
2. Go to **OAuth & Permissions** → **Bot Token Scopes**
3. Add scopes: `channels:history`, `groups:history`, `im:history`, `mpim:history`, `users:read`
4. Install to workspace and copy **Bot User OAuth Token** (starts with `xoxb-`)

```bash
export SLACK_BOT_TOKEN='xoxb-your-bot-token'
```

## Usage

```bash
# Basic usage
slack-thread https://workspace.slack.com/archives/C123/p456789

# With pipes
slack-thread <url> | pbcopy
slack-thread <url> > thread.txt

# Summarize with AI
slack-thread <url> | claude "Summarize this"
slack-thread <url> | claude "Extract action items"
slack-thread <url> | claude "Create Linear issues"
```

## License

MIT