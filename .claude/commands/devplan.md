# /devplan — Generate Development Plan

## What This Command Does

Takes a single issue and produces a complete development plan — the technical roadmap a developer follows from start to finish. Also auto-generates linked backend story and QA story stubs, pre-filled from the issue and SPEC, ready for the developer and QA engineer to complete.

This covers step 7 of the PO workflow: **develop each issue into a development plan**.

---

## When to Use

- After issues have been generated and approved
- Before handing off an issue to a developer
- One run per issue — `/devplan` handles one issue at a time

---

## How to Run

```
/devplan
```

The agent will ask:
1. Which project?
2. Path to issue file (e.g., `projects/<name>/docs/issues/2026-04-10-issue-name.md`)

---

## Execution Steps

1. **Read the issue file** — extract description, acceptance criteria, dependencies, size, SPEC reference
2. **Read the linked SPEC FEAT section** — extract business rules, edge cases, data requirements
3. **Read project context** — `projects/<name>/context.md`
4. **Check for existing stories** in `projects/<name>/docs/stories/` to identify patterns
5. **Run** `skills/docs/prompts/dev_plan.md`
6. **Generate** three documents:
   - Development plan (`templates/dev_plan.md`)
   - Backend story stub (`templates/backend_story.md`)
   - QA story stub (`templates/qa_story.md`)
7. **Update** the issue file's Linked Documents section with paths to all three
8. **Present** all three documents to the user for review
9. **Save** all three files after user approval

---

## Output Files

| Document | Template | Save Location |
|---|---|---|
| Development Plan | `templates/dev_plan.md` | `projects/<name>/docs/issues/YYYY-MM-DD-[issue-slug]-devplan.md` |
| Backend Story | `templates/backend_story.md` | `projects/<name>/docs/stories/YYYY-MM-DD-backend-[issue-slug].md` |
| QA Story stub | `templates/qa_story.md` | `projects/<name>/docs/stories/YYYY-MM-DD-qa-[issue-slug].md` |

---

## Development Plan Contents

- **Technical Approach** — plain-language description of the implementation strategy
- **Implementation Steps** — ordered, independently committable checklist
- **Files / Components Affected** — with change type (new / modify / delete)
- **Dependencies and Integration Points** — services, APIs, DB, config
- **Business Rules to Enforce** — from SPEC, must be verified in code review
- **Effort Breakdown** — hours per area
- **Open Risks** — flagged uncertainties

---

## Next Steps After This Command

| Status | Next Step |
|---|---|
| Dev plan approved | Hand off issue + dev plan + backend story stub to developer |
| After implementation | `/qa` to generate full QA stories and test |
| Risks materialize | Update dev plan, flag in issue |

---

## Guardrails

- One dev plan per issue — do not combine multiple issues
- Business rules section must not be empty — if SPEC has no rules, flag the gap
- Backend story and QA story are stubs — developer and QA fill in the implementation details
- Present all three documents before saving
- Never fabricate stack or architecture details not in project context — flag as TBD instead
- Save location: dev plan in `issues/`, stories in `stories/`
