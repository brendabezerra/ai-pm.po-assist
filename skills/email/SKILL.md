# Email Skill

## Mission

Read, triage, prioritize, categorize, and draft responses for emails across all active projects. Transform inbox noise into structured, actionable information.

## Scope

### Can Do
- Read and list emails (unread, by label, by sender, by date range)
- Triage emails into P1/P2/P3 by project
- Categorize emails (action required, FYI, meeting invite, follow-up, newsletter)
- Draft reply/forward/new email for user review
- Create tasks from emails (using task schema)
- Trigger calendar events from email context (using communication schema)
- Bulk summarize email threads

### Cannot Do
- Send emails without user confirmation
- Delete or permanently archive emails
- Access emails from accounts not configured in MCP
- Modify email labels/filters (manual setup by user)

## Tooling

**`gws` CLI** — Google Workspace CLI, authenticated as `YOUR_GOOGLE_ACCOUNT@domain.com`
- Auth: OAuth 2.0, token stored at `~/.config/gws/credentials.enc`
- All commands run via `Bash(gws *)`

### Key Commands

```bash
# List messages (supports Gmail search syntax in q)
gws gmail users messages list --params '{"userId":"me","maxResults":20,"q":"is:unread"}'
gws gmail users messages list --params '{"userId":"me","maxResults":20,"q":"is:unread after:2024/01/01"}'

# Read full message (format: full | metadata | minimal)
gws gmail users messages get --params '{"userId":"me","id":"MESSAGE_ID","format":"full"}'

# List labels
gws gmail users labels list --params '{"userId":"me"}'

# Create draft
gws gmail users drafts create --params '{"userId":"me"}' --body '{"message":{"raw":"BASE64_RFC2822"}}'

# Send (use only after user confirms)
gws gmail users messages send --params '{"userId":"me"}' --body '{"raw":"BASE64_RFC2822"}'
```

## Rules

1. Always show sender, subject, date, and snippet when listing emails
2. Group emails by project when triaging
3. Never expose full email bodies unless the user asks — show summaries
4. When drafting replies, match the tone of the original thread
5. Flag emails that mention deadlines, blockers, or escalations as P1

## Guardrails

- Sending requires explicit user approval ("Send this?" → Yes)
- Never forward emails to unintended recipients
- Never include sensitive data (passwords, tokens) in draft content
- Rate limit: don't fetch more than 50 emails in a single triage

## Schemas

- `schemas/email_triage.json` — Input/output for triage operations
- `schemas/email_action.json` — Schema for send/reply/forward actions

## Prompts

- `prompts/prioritize.md` — How to assign P1/P2/P3
- `prompts/categorize.md` — How to categorize email types
- `prompts/draft_response.md` — How to draft contextual replies
