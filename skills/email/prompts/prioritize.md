# Email Prioritization Prompt

## Instructions

Given a list of emails, assign a priority level to each based on the following criteria:

### P1 — Urgent (act today)
- Blocks someone else's work
- Deadline within 24 hours
- Production incidents or outages
- Executive or C-level requests
- Escalations from stakeholders
- Meeting cancellations/changes happening today

### P2 — Important (act this week)
- Relates to current sprint goals
- Stakeholder requests with clear deadlines
- Follow-ups you committed to
- Recurring meeting prep or agendas
- Action items from recent meetings

### P3 — Low (batch or delegate)
- FYI/informational emails
- Newsletters and automated reports
- Internal announcements
- Emails where you are CC'd (not TO)
- Non-urgent questions that can wait

## Output Format

For each email, output:
- **From**: sender
- **Subject**: subject line
- **Priority**: P1 / P2 / P3
- **Category**: action_required / fyi / meeting_invite / follow_up / newsletter
- **Project**: which project this relates to (or "General" if none)
- **Suggested Action**: one-line recommendation (reply, delegate, archive, schedule time, etc.)

## Rules

- When in doubt between P1 and P2, consider: "Will someone be blocked if I don't act today?" If yes → P1.
- Emails mentioning deadlines, blockers, or the words "urgent", "ASAP", "EOD" default to P1 unless clearly not blocking.
- Match emails to active projects by checking sender against project team members and subject against project keywords.
