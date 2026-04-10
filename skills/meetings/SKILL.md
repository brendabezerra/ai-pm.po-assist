# Meetings Skill

## Mission

Process meeting notes into structured deliverables: action items, decisions, follow-up messages, task cards, and roadmap change suggestions. Close the loop between meetings and execution.

## Scope

### Can Do
- Accept meeting notes (pasted text, transcripts, or structured input)
- Extract decisions, action items, owners, and deadlines
- Generate structured meeting notes using template
- Create task cards from action items (via task schema)
- Draft follow-up messages for email/WhatsApp (via communication schema)
- Suggest roadmap changes based on meeting outcomes
- Prepare pre-meeting briefs (pull context from project files + calendar)
- Generate document updates based on meeting decisions

### Cannot Do
- Record or transcribe meetings (input must be provided by user)
- Attend meetings on behalf of the user
- Automatically update external tools (Jira, Linear, etc.) without MCP

## MCP Server

None — this skill is prompt-based. It consumes input and produces output that other skills (email, whatsapp, docs) can act on.

## Rules

1. Every action item must have: description, owner, and deadline (ask if missing)
2. Decisions must be recorded with rationale (why was this decided)
3. Follow-up messages should reference the meeting and be ready to send
4. Pre-meeting briefs should include: attendees, agenda, related open action items, project context
5. Always associate meeting output with a project
6. Use the meeting_notes template from `templates/meeting_notes.md`

## Guardrails

- Never fabricate action items or decisions not discussed in the meeting
- Never send follow-ups without user review
- If notes are ambiguous, ask for clarification rather than guessing
- Mark assumptions clearly when interpreting vague notes

## Schemas

- `schemas/meeting_notes.json` — Structured meeting notes input format
- `schemas/action_items.json` — Output format for extracted action items
- `schemas/followup.json` — Output format for follow-up communications

## Prompts

- `prompts/extract_actions.md` — Extract action items from raw notes
- `prompts/generate_tasks.md` — Convert action items into task cards
- `prompts/roadmap_update.md` — Suggest roadmap changes from meeting outcomes
- `prompts/prep_brief.md` — Generate pre-meeting preparation document
