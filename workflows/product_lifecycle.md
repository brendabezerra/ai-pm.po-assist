# Product Lifecycle Workflow

## Overview

The complete end-to-end PO/PM operating model — from stakeholder conversation to code in the development branch. Every step has a command, a template, and a save location.

---

## The 10-Step Workflow

```
Step 1  ──▶  Gather requirements (stakeholder session)
Step 2  ──▶  Cross requirements with project scope
Step 3  ──▶  Analyze conflicts, risks, missing rules
Step 4  ──▶  Write PRD
Step 5  ──▶  Write SPEC
Step 6  ──▶  Break into issues
Step 7  ──▶  Write development plan per issue
Step 8  ──▶  QA testing
Step 9  ──▶  Bug fixing
Step 10 ──▶  Push to development branch
```

---

## Step-by-Step Reference

### Step 1 — Gather Requirements

**Trigger:** Stakeholder meeting, email thread, or chat conversation containing feature requests or change requests.

**Actions:**
1. Take notes during stakeholder session
2. Run `/followup` to extract structured requirements from notes
3. Fill `templates/requirements.md` with extracted requirements
4. Save to `projects/<name>/docs/requirements/YYYY-MM-DD-[feature].md`

**Outputs:**
- Requirements file with REQ-XX entries, business justifications, and acceptance conditions

**Workflow detail:** `workflows/requirements_analysis.md` — Step 1–2

---

### Step 2–3 — Analyze Requirements

**Trigger:** Requirements file complete.

**Command:** `/analyze`

**The agent:**
- Loads project context and existing PRDs
- Classifies each requirement (New / Change / Conflict / Duplicate / Out of scope)
- Identifies business rule conflicts and missing rules
- Produces a risk assessment
- Recommends: Ready / Conditional / Not ready for PRD

**Outputs:**
- Analysis document (shown to PM, not saved unless PM requests)
- List of conflicts and gaps to resolve before PRD

**Workflow detail:** `workflows/requirements_analysis.md` — Step 3–5

---

### Step 4 — Create PRD

**Trigger:** Requirements analysis shows "Ready" or PM resolves all conflicts.

**Command:** `/prd`

**The agent:**
- Loads project context and requirements file
- Generates a full PRD using `templates/prd.md`
- Marks TBD for missing information
- Presents for PM review before saving

**Outputs:**
- PRD saved to `projects/<name>/docs/prds/YYYY-MM-DD-[feature].md`
- Status: `draft` → PM approves → `approved`

---

### Step 5 — Create SPEC

**Trigger:** PRD status = `approved`.

**Command:** `/spec`

**The agent:**
- Reads the approved PRD
- Generates one FEAT section per functional requirement
- Expands each with: user flow, business rules, acceptance criteria, edge cases
- Defines data requirements, interface specs, and error states
- Marks TBD where PRD is silent

**Outputs:**
- SPEC saved to `projects/<name>/docs/specs/YYYY-MM-DD-[feature].md`
- Status: `draft` → PM approves → `approved`

---

### Step 6 — Break into Issues

**Trigger:** SPEC status = `approved`.

**Command:** `/issues`

**The agent:**
- Reads the approved SPEC
- Creates one issue per SPEC FEAT section (splitting large features as needed)
- Assigns size (S/M/L/XL), priority, and sprint
- Maps dependencies between issues
- Outputs summary table + sprint ordering recommendation

**Outputs:**
- N issue files saved to `projects/<name>/docs/issues/YYYY-MM-DD-[issue-slug].md`
- Summary table for sprint planning

---

### Step 7 — Develop Each Issue

**Trigger:** Issue files approved. One per issue, in dependency order.

**Command:** `/devplan`

**The agent:**
- Reads the issue and linked SPEC FEAT section
- Writes technical approach, implementation steps, affected files
- Lists business rules to enforce
- Generates backend story stub and QA story stub

**Outputs (per issue):**
- Dev plan: `projects/<name>/docs/issues/YYYY-MM-DD-[issue]-devplan.md`
- Backend story stub: `projects/<name>/docs/stories/YYYY-MM-DD-backend-[issue].md`
- QA story stub: `projects/<name>/docs/stories/YYYY-MM-DD-qa-[issue].md`

---

### Step 8–9 — QA Testing and Bug Fixing

**Trigger:** Developer marks issue as implemented.

**Command:** `/qa`

**The agent:**
- Completes the QA story with full test scenarios
- Walks PM through each scenario (pass/fail)
- Creates bug reports for failures using `templates/bug_report.md`
- Tracks the fix-and-retest cycle
- Closes QA cycle when all scenarios pass

**Outputs:**
- QA story: `projects/<name>/docs/stories/YYYY-MM-DD-qa-[issue].md`
- Bug reports: `projects/<name>/docs/bugs/YYYY-MM-DD-bug-[slug].md`
- Release checklist: `projects/<name>/docs/YYYY-MM-DD-release-[feature].md`

**Workflow detail:** `workflows/qa_testing.md`

---

### Step 10 — Push to Development Branch

**Trigger:** Release checklist fully signed off.

**Checklist (from `templates/release_checklist.md`):**
- [ ] All issues closed
- [ ] All QA stories passed
- [ ] No open P1 bugs
- [ ] All PRs reviewed and approved
- [ ] Documentation updated
- [ ] Stakeholder sign-off

**Action:** PM authorizes. Developer pushes to development branch.

**Post-push:**
- Update issue statuses to `done`
- Update `projects/<name>/context.md` — sprint goals, key documents
- Archive completed sprint artifacts

---

## Full Document Trail Per Feature

Every feature completed through this workflow produces:

| Document | Template | Location |
|---|---|---|
| Requirements | `requirements.md` | `docs/requirements/` |
| PRD | `prd.md` | `docs/prds/` |
| SPEC | `spec.md` | `docs/specs/` |
| Issues (N files) | `issue.md` | `docs/issues/` |
| Dev Plans (N files) | `dev_plan.md` | `docs/issues/` |
| Backend Stories (N) | `backend_story.md` | `docs/stories/` |
| QA Stories (N) | `qa_story.md` | `docs/stories/` |
| Bug Reports (if any) | `bug_report.md` | `docs/bugs/` |
| Release Checklist | `release_checklist.md` | `docs/` |
| Meeting Notes | `meeting_notes.md` | `docs/meeting-notes/` |

---

## Command Quick Reference

| Step | Command | Input | Output |
|---|---|---|---|
| 1 | `/followup` | Raw meeting notes | Requirements draft |
| 2–3 | `/analyze` | Requirements file | Scope + risk analysis |
| 4 | `/prd` | Requirements + context | PRD |
| 5 | `/spec` | Approved PRD | SPEC |
| 6 | `/issues` | Approved SPEC | N issue files + summary |
| 7 | `/devplan` | Issue file | Dev plan + story stubs |
| 8–9 | `/qa` | Issue + dev plan | QA story + bug reports |
| — | `/daily` | — | Morning briefing |
| — | `/weekly` | — | Week planning |
| — | `/triage` | — | Channel triage |

---

## Guardrails Across the Lifecycle

- A PRD cannot be SPECed until it is `approved`
- A SPEC cannot be broken into issues until it is `approved`
- An issue cannot be QA'd until the developer confirms implementation is complete
- QA cannot be closed until all P1 bugs are resolved
- Release checklist must be signed before pushing to development branch
- Every document has a status field — advance status intentionally, do not skip steps
