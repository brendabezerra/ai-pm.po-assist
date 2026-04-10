# Pre-Meeting Prep Brief Prompt

## Instructions

Generate a preparation document for an upcoming meeting. Pull context from project files, recent meetings, and communication channels.

### Gather

1. **Calendar event details**: title, attendees, agenda (if in description)
2. **Project context**: current sprint goals, open action items from previous meetings
3. **Attendee context**: role, what they care about (from stakeholders.md)
4. **Recent activity**: relevant emails, messages, or decisions since last meeting
5. **Open items**: unresolved action items assigned to meeting attendees

### Output Format

```
## Meeting Prep: [Meeting Title]
**Date**: [Date and Time]
**Project**: [Project Name]

### Attendees
| Name | Role | Key Interest |
|---|---|---|
| | | |

### Agenda
1. [If available from calendar event]

### Context to Know
- [Key facts, recent developments, or decisions relevant to this meeting]

### Open Action Items
| Item | Owner | Deadline | Status |
|---|---|---|---|
| | | | |

### Your Talking Points
- [Suggested points based on your role and open items]

### Questions to Raise
- [Suggested questions based on gaps or blockers]
```

### Rules
- If no agenda is available, suggest one based on project context and open items
- Focus on what the user needs to know and say, not a full project dump
- Highlight items that are overdue or at risk
- Keep it scannable — this is a quick prep read, not a report
