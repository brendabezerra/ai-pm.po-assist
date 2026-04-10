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

| Source | Generates | Template | Command |
|---|---|---|---|
| Stakeholder session (requirements) | Requirements file | `templates/requirements.md` | `/followup` |
| Requirements file + project context | Scope + risk analysis | (shown to user, not saved) | `/analyze` |
| Approved requirements | PRD | `templates/prd.md` | `/prd` |
| Approved PRD | Functional Specification | `templates/spec.md` | `/spec` |
| Approved SPEC | Issues (N files) | `templates/issue.md` | `/issues` |
| Issue file | Dev plan + story stubs | `templates/dev_plan.md` | `/devplan` |
| Issue + dev plan (post-implementation) | QA story + bug reports | `templates/qa_story.md`, `templates/bug_report.md` | `/qa` |
| All issues passed QA | Release checklist | `templates/release_checklist.md` | `/qa` (end of cycle) |
| Technical discussion meeting | Design Doc | `templates/design_doc.md` | — |
| Any meeting | Meeting Notes | `templates/meeting_notes.md` | `/followup` |
| Email with feature request | PRD (draft) | `templates/prd.md` | `/prd` |
| WhatsApp bug report | Bug report | `templates/bug_report.md` | `/qa` |

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
├── requirements/
│   └── YYYY-MM-DD-feature-name.md
├── prds/
│   └── YYYY-MM-DD-feature-name.md
├── specs/
│   └── YYYY-MM-DD-feature-name.md
├── issues/
│   ├── YYYY-MM-DD-issue-name.md
│   └── YYYY-MM-DD-issue-name-devplan.md
├── design-docs/
│   └── YYYY-MM-DD-feature-name.md
├── meeting-notes/
│   └── YYYY-MM-DD-meeting-title.md
├── stories/
│   ├── YYYY-MM-DD-backend-feature-name.md
│   └── YYYY-MM-DD-qa-feature-name.md
└── bugs/
    └── YYYY-MM-DD-bug-description.md
```
