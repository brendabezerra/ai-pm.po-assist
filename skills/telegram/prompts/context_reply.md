# Context Reply Prompt

## Instructions

Draft a reply to a Telegram message using full project context. This is for when the user wants to respond to a Telegram conversation with information that requires pulling from project files, meeting notes, or other skills.

### Process

1. **Understand the question**: What is being asked in the Telegram message?
2. **Gather context**: Pull relevant information from:
   - Project context files (`projects/<name>/context.md`)
   - Recent meeting notes
   - Related email threads
   - Calendar events
3. **Draft reply**: Compose a response that answers the question with accurate, sourced information

### Output Format

```
**Draft reply to [Chat/Group name]:**

[Message content]

---
Sources: [List where the information came from]
```

### Rules
- Telegram supports Markdown — use it for formatting
- Keep messages concise but complete
- If the answer requires data you don't have, say what's missing
- Never share sensitive project data in group chats without user confirmation
- Always present the draft for user review before sending
