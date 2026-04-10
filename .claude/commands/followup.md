# /followup — Post-Meeting Follow-up

You are processing meeting notes and generating follow-up deliverables. Follow the meeting lifecycle in `workflows/meeting_lifecycle.md`.

## Instructions

1. Read `rules/agent_rules.md` for behavioral guidelines.
2. Ask the user for:
   - **Meeting notes**: Paste text, provide a file, or describe what was discussed
   - **Project**: Which project does this meeting belong to? (if not obvious)
   - **Meeting title and date**: If not included in the notes

3. Process the notes:

### Extract
- Apply `skills/meetings/prompts/extract_actions.md` to find:
  - **Decisions** (with rationale)
  - **Action items** (with owners and deadlines)
  - **Blockers** (with impact)

### Generate Deliverables
- **Structured meeting notes** using `templates/meeting_notes.md`
- **Task cards** from action items using `skills/meetings/prompts/generate_tasks.md`
- **Roadmap change suggestions** (if applicable) using `skills/meetings/prompts/roadmap_update.md`

### Draft Follow-ups
- Draft a **follow-up email** summarizing decisions and action items
- Draft **WhatsApp/Telegram messages** for quick notifications (if relevant)
- All drafts presented for user review — never send automatically

## Output

```
# Meeting Follow-up: [Meeting Title] — [Date]
**Project**: [Project Name]

## Decisions
| # | Decision | Rationale | Decided By |
|---|---|---|---|

## Action Items
| # | Action | Owner | Deadline | Priority |
|---|---|---|---|---|

## Blockers
| Blocker | Impact | Owner |
|---|---|---|

## Suggested Roadmap Changes
[If applicable]

## Follow-up Drafts
### Email Draft
[Draft for user review]

### Message Drafts
[WhatsApp/Telegram drafts if applicable]

---
Save meeting notes to: `projects/[project]/docs/meeting-notes/[date]-[title].md`? (y/n)
```
