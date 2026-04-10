# Daily Schedule Prompt

## Instructions

Format today's calendar into a structured briefing for the morning review.

### Output Format

```
## Today's Schedule — [Date]

| Time | Event | Project | Attendees | Prep Needed |
|---|---|---|---|---|
| 09:00-09:30 | Stand-up | Project X | Team | No |
| 10:00-11:00 | Design Review | Project Y | +Stakeholder | Yes — read PRD |

### Conflicts
- [List any overlapping events]

### Prep Required
- **[Event Name]** (HH:MM): [What to prepare]

### Free Blocks
- [List available time blocks of 30min+ for deep work]
```

### Rules
- Sort events chronologically
- Flag events that need preparation: first meetings with new people, presentations, reviews, demos
- Identify conflicts (overlapping times) and suggest which to keep
- Match events to projects by attendee names and event titles
- Highlight free blocks of 30+ minutes as available for deep work
- If an event has a video link, include it
