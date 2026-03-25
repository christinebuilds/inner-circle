# Inner Circle

Your closest people shouldn't need a calendar invite.

Inner Circle is an AI-powered friend scheduler. Tell your Claude (or ChatGPT, or Gemini) to find time with a friend, and it handles the rest — checks your calendar, texts your friend a link, and locks in the plan.

## Quick Start

### 1. Install the skills (30 seconds)

```bash
# Copy both skills to your Claude Code commands
curl -o ~/.claude/commands/inner-circle.md \
  https://raw.githubusercontent.com/christinebuilds/inner-circle/main/commands/inner-circle.md

curl -o ~/.claude/commands/friend-scheduler.md \
  https://raw.githubusercontent.com/christinebuilds/inner-circle/main/commands/friend-scheduler.md
```

### 2. Set up your circle (2 minutes)

Open Claude Code and type `/inner-circle`. It'll walk you through creating your friend list:

```yaml
circle:
  - name: "Maya"
    phone: "+1-555-0101"
    cadence: 14          # days between hangouts
    last_seen: "2026-03-01"
    preferred_contact: "text"
    vibe: "Loves trying new restaurants. Usually free weekends."
    tier: ride-or-die     # ride-or-die | close | keep-warm
```

### 3. Use it

**Check on your people:**
```
> /inner-circle
```
Shows who you haven't seen in too long, drafts casual outreach messages, creates tasks to follow through.

**Schedule a hangout:**
```
> /friend-scheduler
> "find time with Maya for dinner"
```
Checks your calendar, generates a link to text your friend, and locks it in when they respond.

## What You Need

| Feature | Requires |
|---------|----------|
| `/inner-circle` (friend check-ins) | Just the skill file. Works immediately. |
| + Google Tasks integration | [Rube MCP](https://rube.sh) with Google Tasks |
| `/friend-scheduler` (calendar scheduling) | [Rube MCP](https://rube.sh) with Google Calendar + Gmail |

**Don't have Rube?** `/inner-circle` still works great — it shows you who's overdue and drafts messages. You just copy-paste instead of auto-creating tasks. `/friend-scheduler` works in manual mode — you tell it your availability instead of it reading your calendar.

## How Friend Scheduling Works

**You** say "find time with Maya for dinner."

**Your agent** checks your calendar, picks good slots, and generates a link to text Maya.

**Maya** taps the link and sees a clean invite page with your proposed times. Three paths:

1. **Maya has an AI agent** — she copies a prompt, pastes it into her Claude/ChatGPT/Gemini, and her agent checks her calendar and drafts a reply. Done.
2. **Maya doesn't have an agent** — she picks a time and texts you back. Done.
3. **Maya wants her own** — the page links here. The network grows.

## Two Skills

### `/inner-circle` — Who needs you right now?

Scans your friend list and flags:
- **Overdue** — past their cadence, sorted by tier (ride-or-dies first)
- **Soon** — within 7 days of hitting cadence
- **Good** — recently connected

Drafts outreach messages that sound like you, not a CRM. No "I hope this finds you well."

### `/friend-scheduler` — Lock in the plan

Full scheduling assistant with:
- Calendar-aware time proposals
- Friend priority tiers (move things for ride-or-dies, fit in around close friends)
- Agent-to-agent coordination when both people have AI agents
- Email relay for async scheduling
- Recurring plan management

## Works With Any AI Agent

The scheduling protocol (`friend-scheduler-v1`) is platform-agnostic JSON. When your friend taps the invite link, the prompt works in:

- Claude Code
- ChatGPT
- Gemini
- Any LLM with calendar access

## Templates

Copy these to get started:

- [`templates/circle.yaml`](templates/circle.yaml) — example friend list
- [`templates/circle-preferences.yaml`](templates/circle-preferences.yaml) — tone, availability, favorite spots

## Privacy

- All contact info stays local on your machine
- Scheduling only shares available time windows — never event titles or calendar details
- No telemetry, no backend, no accounts
- Your friend list is a YAML file you control

## Contributing

Install it, schedule something with a friend, and tell us what happened. That's the most valuable contribution right now.

Ideas, bugs, or cross-platform implementations welcome — [open an issue](https://github.com/christinebuilds/inner-circle/issues).

---

Built by [Christine Su](https://github.com/christinebuilds)
