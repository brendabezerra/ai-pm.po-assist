# Changelog

All notable changes to the Personal PM Agent are documented here.

## [0.1.0] — 2026-03-31

### Phase 0: Foundation

**Added**
- Root agent definition (`CLAUDE.md`) with role, thinking protocol, skills table, commands, multi-project support, and guardrails
- 6 skill modules with SKILL.md, schemas, prompts, and evals:
  - Email: triage, prioritize, categorize, draft responses
  - Calendar: daily schedule, conflict detection, event management
  - WhatsApp: message reading, action extraction, meeting scheduling
  - Telegram: message reading, context replies, action extraction
  - Meetings: action extraction, task generation, roadmap updates, prep briefs
  - Docs: PRD generation, design docs, story writing
- 3 shared schemas: `communication.json`, `task.json`, `project_context.json`
- 5 templates: PRD, design doc, meeting notes, QA story, backend story
- 4 workflow definitions: daily briefing, weekly planning, meeting lifecycle, documentation flow
- 5 slash commands: `/daily`, `/weekly`, `/triage`, `/followup`, `/prd`
- Multi-project support with `projects/_template/` (context + stakeholders)
- Rules: agent behavior rules and communication style guide
- `.gitignore` for secrets, tokens, sessions, and IDE files
- `.claude/settings.local.json` with base permission configuration

### MCP Servers (planned, not yet configured)
- Google Workspace MCP (`taylorwilsdon/google_workspace_mcp`) — Email + Calendar
- WhatsApp MCP (`jlucaso1/whatsapp-mcp-ts`) — WhatsApp via Baileys
- Telegram MCP (`sparfenyuk/mcp-telegram`) — Telegram via Bot API

---

## Next: Phase 1 — Email + Calendar
- Set up Google Workspace MCP with OAuth
- Configure email and calendar skills with live data
- Test `/daily` and `/triage` commands end-to-end
