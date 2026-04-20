# Inner Circle

AI-powered friend scheduler — helps Christine stay connected with her closest people without calendar overhead.

## What This Is

Public repo: `christinebuilds/inner-circle`
A skill + web app that checks who you haven't seen in too long, drafts outreach, and handles scheduling via shared links.

## Architecture

- `commands/` — Claude Code skills (`/inner-circle`, `/friend-scheduler`)
- `web/` — Scheduling link web app (invite page)
- `invite.html` — Standalone invite page
- `templates/` — Message templates for outreach

## Data

- Friend list: `~/Coding/notes/projects/inner-circle/circle.yaml`
- Preferences: `~/Coding/notes/projects/inner-circle/preferences.yaml`
- Responses tracked in Supabase: `icknhfkfgeitbzgpomwh.supabase.co`

## How It Works

1. `/inner-circle` — scans circle.yaml, finds who's overdue based on cadence + last_seen
2. Drafts casual outreach messages (text-style, not formal)
3. `/friend-scheduler` — checks Google Calendar for free slots, generates invite link
4. Friend clicks link → picks a time → confirmed in Supabase → syncs to calendar

## Friend Tiers

- **ride-or-die** — see every 1-2 weeks, highest priority
- **close** — every 2-4 weeks
- **keep-warm** — monthly+, light touch

## MCP Connections Needed

- Google Calendar (free/busy checks)
- Supabase (response tracking)

## Context

Christine is in SF, has a toddler (Ava), expecting second child. Scheduling is hard — the whole point is to make friend maintenance effortless. Tone of outreach should be warm and casual, never transactional.
