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

## [0.2.0] — 2026-04-10

### Phase 1: Full Product Development Lifecycle

**Added — Slash Commands (5 new)**
- `/analyze` — Requirements analysis: cross-checks stakeholder requirements against project scope, surfaces conflicts, missing rules, scope gaps, and risks before PRD writing (steps 2–3 of PO workflow)
- `/spec` — Functional Specification generator: transforms an approved PRD into a SPEC that bridges intent and implementation detail (step 5)
- `/issues` — SPEC decomposition: breaks a SPEC into discrete, sized, and prioritized issues ready for sprint planning, one file per issue plus a summary table (step 6)
- `/devplan` — Development plan generator: produces a full technical roadmap per issue and auto-generates linked backend story and QA story stubs (step 7)
- `/qa` — QA test cycle: generates QA test stories, guides test execution, creates bug reports for failures, and tracks pass/fail status until issue is verified (steps 8–9)

**Added — Prompts (`skills/docs/prompts/`)**
- `requirements_analysis.md` — prompt for cross-checking requirements against scope and business rules
- `spec.md` — prompt for generating functional specifications from PRDs
- `issue_writer.md` — prompt for decomposing SPEC sections into individual issues
- `dev_plan.md` — prompt for generating per-issue development plans and story stubs

**Added — Templates (6 new)**
- `requirements.md` — raw requirements capture from stakeholder sessions
- `spec.md` — Functional Specification (bridge between PRD and development)
- `issue.md` — individual issue/ticket derived from SPEC
- `dev_plan.md` — development plan per issue with story stubs
- `bug_report.md` — bug report from QA testing
- `release_checklist.md` — definition-of-done checklist before pushing to dev branch

**Added — Workflows (3 new)**
- `product_lifecycle.md` — complete 10-step end-to-end PO/PM operating model (requirements → code in dev branch)
- `requirements_analysis.md` — steps 1–3: stakeholder session → requirements capture → `/analyze` → sign-off
- `qa_testing.md` — steps 8–9: implementation done → `/qa` → bug reports → re-test → close issue

**Updated**
- `workflows/documentation_flow.md` — extended to cover the full SPEC → issues → devplan → QA chain
- `skills/docs/SKILL.md` — added scope for spec, issue, devplan, and QA prompts
- `CLAUDE.md` — added 5 new commands to the commands table and 6 new templates to the templates list
- `README.md` — major expansion covering the full product workflow, all commands, templates, and workflows

**Added — Workspaces**
- `workspaces/operational/design` — operational workspace for design artifacts

---

## Next: Phase 2 — MCP Integrations
- Set up Google Workspace MCP with OAuth (Email + Calendar)
- Configure WhatsApp and Telegram MCP servers
- Test `/daily` and `/triage` commands end-to-end with live data
