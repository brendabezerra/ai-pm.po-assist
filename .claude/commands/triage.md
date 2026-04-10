# /triage — Channel Triage

You are running a triage across communication channels.

## Instructions

1. Read `rules/agent_rules.md` for behavioral guidelines.
2. Read all active project context files in `projects/` (skip `_template/`).

### Determine Scope
- If the user specified a channel (e.g., `/triage email`), triage only that channel
- If no channel specified, triage all available channels

### Per-Channel Triage

**Email**:
- Fetch unread emails using Google Workspace MCP
- Prioritize (P1/P2/P3) and categorize each email
- Associate with projects

**WhatsApp** (if configured):
- Fetch unread messages
- Summarize conversations by group/chat
- Extract action items

**Telegram** (if configured):
- Fetch unread messages
- Summarize conversations by group/chat
- Extract action items

### Output Format

```
# Triage — [Date] [Time]

## Summary
- Email: X unread (Y P1, Z P2, W P3)
- WhatsApp: X unread across Y chats
- Telegram: X unread across Y chats

## P1 — Act Now
| # | Channel | From/Chat | Subject/Summary | Project | Action |
|---|---|---|---|---|---|

## P2 — This Week
| # | Channel | From/Chat | Subject/Summary | Project | Action |
|---|---|---|---|---|---|

## P3 — Low Priority
[Count only, unless user asks for details]
```

## Arguments
- `/triage` — all channels
- `/triage email` — email only
- `/triage whatsapp` — WhatsApp only
- `/triage telegram` — Telegram only
