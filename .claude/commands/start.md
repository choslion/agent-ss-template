---
description: Start a session — brief on current state
---

Start the session. Proceed in this order:

1. If this workspace is a git repository with a remote, run `git pull` to get the
   latest memory (another machine may have updated it). If it fails or there are
   conflicts, tell the user instead of guessing. If there's no git repo, skip this.
2. Read `state/current.md`, `state/todos.md`, and `state/goals.md`.
3. Read the most recent log in the `sessions/` folder.
4. Check today's date.
5. Give a briefing:
   - What was in progress last session and what wasn't finished
   - Upcoming deadlines or items needing attention
   - 1–3 recommended priorities for today

Keep the briefing under 10 lines. End with "What should we start with today?"
