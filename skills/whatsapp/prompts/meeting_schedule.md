# Meeting Schedule from WhatsApp Prompt

## Instructions

When a WhatsApp conversation contains a meeting request or scheduling discussion, extract the meeting details and prepare a calendar event.

### Extraction

From the conversation, identify:
1. **What**: Meeting topic/purpose
2. **Who**: Participants mentioned
3. **When**: Proposed date/time (convert relative references like "tomorrow", "next Tuesday" to absolute dates)
4. **Where**: Location or "virtual" (include video link if mentioned)
5. **Project**: Which project this relates to

### Output

Generate a calendar event object following `skills/calendar/schemas/event_manage.json` with action: "create".

Also draft a confirmation message back to the WhatsApp chat:
```
Confirmed: [Meeting topic]
Date: [Date and time]
Attendees: [Names]
Link: [Video link if applicable]
```

### Rules
- If date/time is ambiguous, ask the user to confirm before creating
- If attendees are mentioned by first name only, match against project team members
- Always create the event as a draft requiring user confirmation
- Include the WhatsApp chat context in the event description for reference
