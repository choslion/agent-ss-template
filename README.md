# SS — Personal AI Assistant Template

A personal "Chief of Staff" agent built on [Claude Code](https://claude.com/claude-code),
inspired by [marvin-template](https://github.com/SterlingChin/marvin-template).
It remembers context across sessions, tracks your goals and todos, and briefs you
when you come back — even days later.

There is no code here. The entire agent is a ruleset (`CLAUDE.md` + slash commands)
plus markdown files that accumulate as its memory.

## Getting Started

1. Clone this repo (give it any name you like):
   ```
   git clone https://github.com/choslion/agent-ss-template.git my-assistant
   cd my-assistant
   ```
2. Open it in Claude Code — run `claude` in the folder (or double-click `SS.bat` on Windows).
3. Say hi. SS walks you through onboarding (your name, goals, preferred style).
4. From then on: start each session with `/start`, end with `/end`. That's the whole habit.

> **Keep your copy private.** Your goals, todos, and session logs are stored as
> plain markdown in this folder. If you push it to GitHub, use a private repo —
> then your assistant's memory syncs across machines for free.

## Commands

| Command | Description |
|---------|-------------|
| `/start` | Pick up from last session + today's briefing |
| `/update` | Mid-session checkpoint |
| `/status` | Goals / todos / decisions at a glance |
| `/end` | Save session log + update state (+ git sync if you set up a repo) |
| `/help` | Usage guide |

## How It Works

```
.
├── CLAUDE.md              # SS's identity, principles, session protocol (auto-loaded)
├── .claude/commands/      # Slash command definitions (markdown)
├── profile/me.md          # Who you are, how you like to communicate
├── state/
│   ├── current.md         # Handoff doc between sessions
│   ├── goals.md           # Long-term goals + progress
│   ├── todos.md           # Task list
│   └── decisions.md       # Decision log with reasoning
└── sessions/              # Per-date session logs (YYYY-MM-DD.md)
```

Claude Code automatically loads `CLAUDE.md` at the start of every session. It tells
SS to read `state/` and the latest session log — that's what makes conversations
continuous. `/end` writes the session back to disk. Memory is just files: you can
read it, edit it, delete it, or back it up.

## Extending

- **New command**: drop a markdown file in `.claude/commands/` (or just ask SS to make one).
- **Integrations**: connect Google Calendar, Notion, Slack, etc. via MCP servers (`claude mcp add`).
- **Style**: edit `profile/me.md` to change how SS talks to you.
- **Model**: `SS.bat` defaults to Sonnet; change the `--model` flag or use `/model` in-session.

## License

MIT — use it, fork it, rename it.
