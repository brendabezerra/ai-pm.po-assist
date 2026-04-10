# Daily Briefing Workflow

## Trigger
User runs `/daily` command each morning.

## Steps

### Step 1: Email Triage
1. Fetch unread emails using Google Workspace MCP
2. Apply `skills/email/prompts/prioritize.md` to assign P1/P2/P3
3. Apply `skills/email/prompts/categorize.md` to classify types
4. Associate each email with a project (match sender/subject against `projects/`)

### Step 2: Calendar Review
1. Fetch today's events using Google Workspace MCP
2. Apply `skills/calendar/prompts/daily_schedule.md` to format
3. Apply `skills/calendar/prompts/conflict_check.md` to detect issues
4. Flag events needing preparation

### Step 3: Messaging Triage (when MCP servers are configured)
1. Fetch unread WhatsApp messages using WhatsApp MCP
2. Fetch unread Telegram messages using Telegram MCP
3. Summarize by project and extract action items
4. Flag messages requiring responses

### Step 4: Priority Synthesis
1. Aggregate P1 items from all channels
2. Generate **Top 5 Priorities** ranked by urgency and impact
3. Suggest time blocks for each priority based on available calendar slots

## Output Format

```
# Daily Briefing — [Date]

## Top 5 Priorities
1. [Priority item] — [Source: email/meeting/message] — [Suggested time block]
2. ...

## Email Triage
| # | From | Subject | Priority | Category | Project | Action |
|---|---|---|---|---|---|---|
| 1 | | | P1 | | | |

**Summary**: X unread → Y P1, Z P2, W P3

## Today's Schedule
[Output from daily_schedule prompt]

## Messages Requiring Attention
### WhatsApp
- [Group/Chat]: [Summary] — [Action needed]

### Telegram
- [Group/Chat]: [Summary] — [Action needed]

## Free Blocks for Deep Work
- [Time ranges]
```

## Dependencies
- Google Workspace MCP (required for email + calendar)
- WhatsApp MCP (optional — skip gracefully if not configured)
- Telegram MCP (optional — skip gracefully if not configured)
- Active project context files in `projects/`
