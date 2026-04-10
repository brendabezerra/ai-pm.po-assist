# Meeting Lifecycle Workflow

## Overview
The full meeting lifecycle: **Prep → Meeting → Notes → Actions → Follow-up → Documentation**

## Phase 1: Pre-Meeting Prep
**Trigger**: User asks for meeting prep, or `/daily` identifies an upcoming meeting needing prep.

1. Read calendar event details (attendees, agenda, time)
2. Pull project context and stakeholder info
3. Check open action items for attendees
4. Generate prep brief using `skills/meetings/prompts/prep_brief.md`

## Phase 2: During Meeting
**Agent is passive** — the user takes notes manually or uses a transcription tool.

## Phase 3: Post-Meeting Processing
**Trigger**: User runs `/followup` with meeting notes.

1. Accept raw meeting notes (pasted text or file)
2. Extract action items using `skills/meetings/prompts/extract_actions.md`
3. Extract decisions and blockers
4. Generate structured meeting notes using `templates/meeting_notes.md`

## Phase 4: Task Generation
1. Convert action items to task cards using `skills/meetings/prompts/generate_tasks.md`
2. Associate tasks with the correct project
3. Suggest roadmap changes if applicable using `skills/meetings/prompts/roadmap_update.md`

## Phase 5: Follow-up Communication
1. Draft follow-up email with meeting summary + action items
2. Draft WhatsApp/Telegram messages for quick notifications
3. All drafts require user confirmation before sending

## Phase 6: Documentation
1. Save structured meeting notes to project directory
2. Update project context if sprint goals or priorities changed
3. Generate or update PRDs/design docs if meeting produced new requirements

## Cross-Skill Data Flow

```
Calendar Event → Prep Brief (meetings skill)
                      ↓
Raw Notes → Action Items (meetings skill)
                      ↓
            ┌─────────┼─────────┐
            ↓         ↓         ↓
      Task Cards  Follow-up   Meeting Notes
      (task.json) Emails/Msgs (local markdown)
                  (comm.json)
```
