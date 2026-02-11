# Druid

Druid is a Discord bot built with Pycord and MongoDB. It bundles temporary voice channels, auto-moderation, and an XP/leveling system into one service.

## Features

- Temporary voice channel system with owner controls (`/voice ...`)
- Word-based auto moderation (`/automod ...`)
- XP + level tracking with leaderboards (`/xp ...`)
- Basic utility commands (`/ping`, `/help`)

## Tech Stack

- Python 3.12
- [Pycord](https://docs.pycord.dev/)
- MongoDB (via `pymongo`)
- Pipenv
- Optional Docker / Docker Compose

## Project Structure

```text
main.py                  # entrypoint
src/__init__.py          # bot setup, intents, dynamic cog loading
src/cogs/core.py         # /ping, /help
src/cogs/temp_voice.py   # temporary voice channel system
src/cogs/auto_moderation.py
src/cogs/levelling.py
database/__init__.py     # MongoDB access layer
logger/__init__.py       # logging config
error/__init__.py        # custom exceptions
statics/interface.png    # UI image used by /voice setup
```

## Requirements

- Python `3.12`
- A Discord bot token
- A MongoDB connection URI
- Discord bot permissions for:
  - slash commands
  - managing channels/permissions
  - moving members
  - deleting messages (for automod)

## Configuration

The bot reads environment variables directly with `os.getenv`.

Required:

- `discord_token`
- `mongodb_uri`

Optional (currently not used by runtime code):

- `guild_id`

Example:

```bash
export discord_token="YOUR_DISCORD_BOT_TOKEN"
export mongodb_uri="YOUR_MONGODB_URI"
```

## Local Development

1. Install dependencies:

```bash
pipenv install
```

2. Set required environment variables in your shell.
3. Start the bot:

```bash
pipenv run python main.py
```

## Docker

Build and run with compose:

```bash
docker compose up --build
```

`docker-compose.yml` expects an `.env` file in the project root.

## Commands

### Core

- `/ping`
- `/help`

### Temporary Voice (`/voice`)

- `/voice setup`
- `/voice reset`
- `/voice cleanup`
- `/voice rename <new_name>`
- `/voice limit <number>`
- `/voice privacy`
- `/voice kick`
- `/voice block`
- `/voice unblock`
- `/voice invite`

### Auto Moderation (`/automod`)

- `/automod add_bad_word <word>` (manage channels permission)
- `/automod remove_bad_word <word>` (manage channels permission)
- `/automod list_bad_words`

### XP System (`/xp`)

- `/xp leaderboard`
- `/xp rank [user]`
- `/xp profile [user]`
- `/xp add_xp <user> <xp>` (administrator permission)
- `/xp remove_xp <user> <xp>` (administrator permission)
- `/xp reset_xp <user>` (administrator permission)
- `/xp reset_level <user>` (administrator permission)
- `/xp reset_all` (administrator permission)
- `/xp reset_leaderboard` (administrator permission)

## Logging

- Logs are configured in `logger/__init__.py`
- Output files:
  - `logger/logs/bot.log`
  - `logger/logs/database.log`

## License

See `LICENSE`.
