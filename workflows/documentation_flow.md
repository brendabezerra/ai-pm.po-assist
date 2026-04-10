# Documentation Flow Workflow

## Overview
How information from meetings, emails, and conversations becomes structured project documentation.

## Flow

```
Source (any channel)
    ↓
Extract (relevant skill)
    ↓
Structure (docs skill + template)
    ↓
Review (user approval)
    ↓
Save (local markdown → future: Confluence)
```

## Triggers

| Source | Generates | Template |
|---|---|---|
| Meeting with new requirements | PRD | `templates/prd.md` |
| Technical discussion meeting | Design Doc | `templates/design_doc.md` |
| Sprint planning meeting | Backend + QA Stories | `templates/backend_story.md`, `templates/qa_story.md` |
| Any meeting | Meeting Notes | `templates/meeting_notes.md` |
| Email with feature request | PRD (draft) | `templates/prd.md` |
| WhatsApp bug report | QA Story | `templates/qa_story.md` |

## Process

### 1. Capture
- Meeting notes → extracted via `/followup`
- Email content → flagged during `/triage` or `/daily`
- Chat messages → flagged during channel triage

### 2. Transform
- Apply the appropriate template
- Fill with extracted content
- Mark unknowns as TBD
- Cross-reference with project context

### 3. Review
- Present document to user for review
- User edits, approves, or requests changes
- Never publish without approval

### 4. Store
- Save to local project directory: `projects/<name>/docs/`
- Future: sync to Confluence space

### 5. Link
- Update project context file with reference to new document
- Link related documents (PRD → Design Doc → Stories)

## Naming Convention

```
projects/<project-slug>/docs/
├── prds/
│   └── YYYY-MM-DD-feature-name.md
├── design-docs/
│   └── YYYY-MM-DD-feature-name.md
├── meeting-notes/
│   └── YYYY-MM-DD-meeting-title.md
└── stories/
    ├── YYYY-MM-DD-backend-feature-name.md
    └── YYYY-MM-DD-qa-feature-name.md
```
