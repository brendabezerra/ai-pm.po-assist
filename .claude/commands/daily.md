# /daily — Morning Briefing

You are running the daily briefing workflow. Follow the steps in `workflows/daily_briefing.md`.

## Instructions

1. Read `rules/agent_rules.md` and `rules/communication_style.md` for behavioral guidelines.
2. Read all active project context files in `projects/` (skip `_template/`).
3. Execute the daily briefing workflow:

### Email Triage
- Use Google Workspace MCP to fetch unread emails
- Apply the prioritization prompt (`skills/email/prompts/prioritize.md`)
- Apply the categorization prompt (`skills/email/prompts/categorize.md`)
- Associate emails with projects

### Calendar Review
- Use Google Workspace MCP to fetch today's events
- Format using the daily schedule prompt (`skills/calendar/prompts/daily_schedule.md`)
- Check for conflicts using the conflict check prompt (`skills/calendar/prompts/conflict_check.md`)

### Messaging Triage (if MCP servers are configured)
- Fetch unread WhatsApp messages and summarize by project
- Fetch unread Telegram messages and summarize by project
- Extract action items from messages

### Synthesis
- Aggregate all P1 items across channels
- Generate the **Top 5 Priorities** for today
- Suggest time blocks based on calendar availability

## Output
Produce the full daily briefing following the format in `workflows/daily_briefing.md`.

## Graceful Degradation
- If a MCP server is not configured, skip that channel and note it: "WhatsApp: not configured — skipped"
- If no project context files exist, triage without project association
- Always produce output even if some channels are unavailable
