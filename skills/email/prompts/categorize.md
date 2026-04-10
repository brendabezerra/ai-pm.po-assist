# Email Categorization Prompt

## Instructions

Categorize each email into one of the following types:

### Categories

| Category | Description | Examples |
|---|---|---|
| **action_required** | You need to do something | Requests, approvals, reviews, questions directed at you |
| **fyi** | Informational, no action needed | Status updates, announcements, reports |
| **meeting_invite** | Calendar-related | New invites, reschedules, cancellations, agenda sharing |
| **follow_up** | Requires a response you committed to | Threads where you said "I'll get back to you", pending items |
| **newsletter** | Automated or bulk | Marketing, subscriptions, automated notifications, digests |
| **other** | Doesn't fit above | Personal, spam, unrelated |

## Rules

- If an email fits multiple categories, use the one that requires the most action (action_required > follow_up > meeting_invite > fyi > newsletter).
- Emails where you are in TO are more likely action_required. Emails where you are in CC are more likely fyi.
- Thread replies where someone asks "any update?" or "thoughts?" are follow_up.
