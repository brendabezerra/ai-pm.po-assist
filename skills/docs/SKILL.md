# Docs Skill

## Mission

Generate and maintain project documentation — PRDs, design docs, user stories, and other deliverables. Transform project context and meeting outcomes into polished, structured documents.

## Scope

### Can Do
- Generate PRDs from project context and requirements
- Generate design documents from technical discussions
- Write user stories (QA and Backend) from feature descriptions
- Update existing documents with new information
- Create documents from meeting notes and action items
- Save documents locally as markdown files
- Use templates from `templates/` as starting structures
- Analyze requirements against project scope and existing business rules (conflict detection, risk assessment)
- Generate Functional Specifications (SPEC) from approved PRDs
- Break SPECs into sized, prioritized issues
- Generate development plans per issue (with backend story and QA story stubs)

### Cannot Do
- Publish to Confluence (deferred to Phase 6)
- Create visual diagrams or mockups
- Access external document systems without MCP
- Auto-update documents without user review

## MCP Server

**Current**: None — all documents are local markdown files.
**Future (Phase 6)**: Atlassian MCP (`atlassian/atlassian-mcp-server`) for Confluence read/write.

## Rules

1. Always use the appropriate template from `templates/` as the starting structure
2. Every document must specify: project, author, date, and status
3. PRDs must include: problem statement, goals, scope, requirements, and timeline
4. Design docs must include: context, proposed design, alternatives considered, and testing strategy
5. Stories must include: acceptance criteria, test scenarios, and dependencies
6. Mark assumptions vs. confirmed facts clearly
7. Save documents in a logical location (project directory or templates output)

## Guardrails

- Never publish documents externally without user confirmation
- Never remove content from existing documents without asking
- Always show a diff/summary of changes when updating existing docs
- Clearly label draft vs. approved status

## Schemas

- `schemas/doc_create.json` — Schema for document creation requests
- `schemas/doc_update.json` — Schema for document update requests

## Prompts

- `prompts/design_doc.md` — Generate design documents
- `prompts/prd.md` — Generate PRDs
- `prompts/story_writer.md` — Write QA and Backend stories
- `prompts/requirements_analysis.md` — Analyze requirements vs. scope, conflicts, risks
- `prompts/spec.md` — Generate Functional Specification from PRD
- `prompts/issue_writer.md` — Break SPEC into issues
- `prompts/dev_plan.md` — Generate development plan per issue
