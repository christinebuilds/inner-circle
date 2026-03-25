---
description: Stay connected with your closest people — the ones who shouldn't need a calendar invite. Surfaces who you haven't seen in too long, drafts casual outreach, and creates tasks to follow through. Use when the user says "inner circle", "who haven't I seen", "friend check", "reach out to people", or invokes /inner-circle.
---

# Inner Circle — Your People Shouldn't Need a Calendar Invite

Your calendar is full of meetings. This isn't about those people. This is about the friends who matter most — the ones you keep meaning to text back, the ones where "we should hang out soon" has been sitting in your head for weeks.

Your job is to:
1. Check who you haven't seen in too long
2. Draft real, human outreach messages — not calendar invites
3. Make it easy to actually follow through

---

## Step 0 — Load Your Circle

Read the inner circle list at `~/Coding/notes/projects/inner-circle/circle.yaml`.

Expected format:
```yaml
circle:
  - name: "Alex Kim"
    phone: "+1..."
    email: "alex@example.com"
    cadence: 14  # days — how often you ideally see or talk to this person
    last_seen: "2026-02-28"
    preferred_contact: "text"  # text | email | call | voice-memo
    vibe: "Likes hiking. Works in Soma. Down for spontaneous plans."
    tier: ride-or-die  # ride-or-die | close | keep-warm

  - name: "Jordan Lee"
    cadence: 30
    last_seen: "2026-01-15"
    preferred_contact: "email"
    vibe: "Lives in NYC. Catch up over video calls. Loves food recs."
    tier: close
```

**Tier definitions:**
- **ride-or-die** — Your absolute closest. If it's been too long, this is a red flag. Surface these first, always.
- **close** — Real friends you actively want in your life. Regular cadence matters.
- **keep-warm** — People you care about but see less often. Longer cadence is fine.

If the file doesn't exist, offer to scaffold it:
- Create `~/Coding/notes/projects/inner-circle/circle.yaml` with example entries across all three tiers
- Create `~/Coding/notes/projects/inner-circle/overview.md`

Also check for preferences at `~/Coding/notes/projects/inner-circle/preferences.yaml`:
- Default message tone (casual, warm, funny)
- Typical availability (weekday evenings, weekends, flexible)
- Home base / neighborhood (for suggesting spots)

---

## Step 1 — Who Needs You Right Now?

For each person, calculate days since `last_seen` vs their `cadence`.

**Classify into:**

**OVERDUE** — Past their cadence. Sorted by: ride-or-die first, then by how far past due.

**SOON** — Within 7 days of hitting cadence. Reach out now and it won't become overdue.

**GOOD** — Recently connected. No action needed.

If a ride-or-die is more than 2x past cadence, flag it prominently — that's the kind of drift that happens without you noticing.

---

## Step 2 — Draft Messages That Sound Like You

For each OVERDUE and SOON person, draft a message that:
- Matches their `preferred_contact` (texts: short and casual. Emails: slightly longer but still warm. Calls: suggest a specific time.)
- Uses their `vibe` to personalize — mention something they'd actually respond to
- Suggests something **specific**: a place, an activity, a time window. Not "let's catch up sometime."
- Uses `[PLACEHOLDER]` for anything you'd need to confirm (exact date, restaurant choice)

**The vibe is:** you're texting a friend, not scheduling a stakeholder meeting. No "I hope this finds you well." No "per my last message."

**Good examples:**
> hey! lands end saturday morning? i'll bring coffee

> it's been way too long — dinner this week? you pick the spot

> video call this weekend? i want to hear about the new job

**Bad examples:**
> Hi Alex, I wanted to reach out because it's been 23 days since we last connected...

> I hope you're doing well! I was wondering if you might be available...

---

## Step 3 — Create Tasks (if Google Tasks is connected)

Check if Google Tasks is available via `RUBE_MANAGE_CONNECTIONS`.

If connected:
1. Use `GOOGLETASKS_LIST_TASK_LISTS` to get the task list ID
2. Use `GOOGLETASKS_BULK_INSERT_TASKS` to create one task per person:
   - `title`: "Text [Name]" or "Call [Name]" (match their preferred contact)
   - `notes`: The drafted message + any context
   - `due`: Tomorrow (creates gentle urgency)

If not connected, just present the messages — the user can copy-paste or send manually.

---

## Step 4 — Quick Update

Ask: **"Have you actually seen anyone on this list recently? I'll update the dates."**

If they mention names, update `last_seen` in `circle.yaml`. Accept:
- "Saw Alex last Tuesday" → calculate the date
- "Had dinner with Alex and Jordan" → update both
- "Alex — yesterday" → use yesterday's date

---

## Step 5 — The Rundown

```
## Inner Circle Check-In — [Date]

### Needs Attention
🔴 **[Name]** — [X days] since last seen (you usually see them every [Y days])
   [preferred_contact emoji] "[draft message]"

### Reach Out Soon
🟡 **[Name]** — due in [X days]
   [preferred_contact emoji] "[draft message]"

### You're Good
🟢 [Name] (saw [X days ago]) · [Name] (saw [X days ago]) · ...

---
[X] messages drafted · [Y] tasks created · [Z] ride-or-dies checked on
```

Use these emoji for contact methods: 📱 text · 📧 email · 📞 call · 🎤 voice memo

---

## Notes

- **This is not a CRM.** Don't treat it like one. No "engagement scores." No "touchpoints." These are friends.
- **Ride-or-die alerts**: If a ride-or-die person is 2x+ overdue, add a prominent note. These are the relationships that matter most.
- **Group hangs count**: If someone mentions a group hangout, update everyone who was there.
- **No guilt**: Never frame messages as "it's been X days." The drafts should sound like you just thought of them — because you did.
- **Privacy**: All contact info stays local. Never send it anywhere beyond the user's configured integrations (Google Tasks).
- **Timezone**: User is in San Francisco (PT). Use PT dates.
