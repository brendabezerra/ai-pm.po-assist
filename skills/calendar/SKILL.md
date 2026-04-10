# Calendar Skill

## Mission

Manage the user's schedule by reading events, detecting conflicts, preparing meeting briefs, and creating/editing events. Ensure the user is always prepared and never double-booked.

## Scope

### Can Do
- Read today's/this week's/custom range calendar events
- Detect scheduling conflicts
- Prepare pre-meeting briefs (who's attending, agenda, related project context)
- Create new events (with user confirmation)
- Edit existing events (reschedule, add attendees, update description)
- Cancel events (with user confirmation)
- Suggest optimal meeting times based on availability
- Send WhatsApp/email notifications about calendar changes

### Cannot Do
- Create events without user confirmation
- Access calendars not configured in MCP
- Manage other people's calendars directly
- Auto-decline meetings

## Tooling

**`gws` CLI** — Google Workspace CLI, authenticated as `YOUR_GOOGLE_ACCOUNT@domain.com`
- Auth: OAuth 2.0, token stored at `~/.config/gws/credentials.enc`
- All commands run via `Bash(gws *)`

### Key Commands

```bash
# List events for a date range (ISO 8601 with timezone)
gws calendar events list --params '{"calendarId":"primary","timeMin":"2026-04-02T00:00:00-03:00","timeMax":"2026-04-02T23:59:59-03:00","singleEvents":true,"orderBy":"startTime"}'

# Get single event
gws calendar events get --params '{"calendarId":"primary","eventId":"EVENT_ID"}'

# Create event (requires user confirmation before running)
gws calendar events insert --params '{"calendarId":"primary"}' --body '{"summary":"Title","start":{"dateTime":"2026-04-03T10:00:00-03:00","timeZone":"America/Recife"},"end":{"dateTime":"2026-04-03T11:00:00-03:00","timeZone":"America/Recife"},"attendees":[{"email":"someone@example.com"}]}'

# Update event (requires user confirmation)
gws calendar events update --params '{"calendarId":"primary","eventId":"EVENT_ID"}' --body '{...}'

# Delete event (requires user confirmation)
gws calendar events delete --params '{"calendarId":"primary","eventId":"EVENT_ID"}'

# List all calendars
gws calendar calendarlist list
```

## Rules

1. Always show event title, time, attendees, and location when listing events
2. Highlight events that need preparation (first meeting with stakeholder, presentation, review)
3. Flag scheduling conflicts immediately
4. When creating events, always include: title, time, attendees, description, and video link if remote
5. Associate events with projects when possible (match by attendees, title keywords, or user input)

## Guardrails

- Creating, editing, or canceling events requires user confirmation
- Never share calendar details with external parties
- Never auto-accept or auto-decline invitations
- Always confirm timezone when scheduling across regions

## Schemas

- `schemas/event_read.json` — Schema for reading and filtering events
- `schemas/event_manage.json` — Schema for create/edit/cancel operations

## Prompts

- `prompts/daily_schedule.md` — Format today's schedule for the daily briefing
- `prompts/conflict_check.md` — Detect and report scheduling conflicts
