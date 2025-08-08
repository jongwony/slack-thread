# slack-thread

Unix-style tool to fetch Slack thread conversations for piping to other tools.

## Installation

```bash
# Download and install
curl -L https://raw.githubusercontent.com/jongwony/slack_thread/main/slack-thread -o /usr/local/bin/slack-thread
chmod +x /usr/local/bin/slack-thread

# Or clone and symlink
git clone https://github.com/jongwony/slack_thread
ln -s $(pwd)/slack_thread/slack-thread /usr/local/bin/slack-thread
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
slack-thread <url> | claude "Summarize this"
slack-thread <url> | pbcopy
slack-thread <url> > thread.txt

# Verbose mode
slack-thread -v <url>
```

## Examples

```bash
# Summarize with AI
slack-thread <url> | claude "Extract action items"

# Search in thread
slack-thread <url> | grep -i "deadline"

# Count messages
slack-thread <url> | wc -l
```

## License

MIT