# Development Plan Prompt

## Purpose

Transform a single issue into a complete development plan — the technical roadmap a developer follows to implement the issue from start to finish. Also generates stubs for the linked backend story and QA story so they are ready to be filled in.

---

## Inputs Required

1. **Issue file** — path to `projects/<name>/docs/issues/YYYY-MM-DD-issue-name.md`
2. **Parent SPEC** — linked in the issue file; read the relevant FEAT section
3. **Project context** — `projects/<name>/context.md` (team, stack, current sprint)
4. **Existing backend stories** (optional) — check `projects/<name>/docs/stories/` for patterns to reuse

---

## Generation Steps

### Step 1 — Understand the Issue

From the issue file, extract:
- What the feature does (description and user story)
- All acceptance criteria
- All dependencies (blocked by / blocks)
- Size estimate and priority
- The SPEC FEAT section it maps to

### Step 2 — Define the Technical Approach

Write a plain-language description of:
- The core mechanism (what the implementation will do)
- What existing patterns, components, or modules will be reused (reference project context for known stack details)
- What will be built from scratch
- The data flow (where data comes from, how it is transformed, where it goes)

Keep this section implementation-aware but technology-agnostic — do not prescribe a specific library or framework unless the project context specifies one.

### Step 3 — Break Into Implementation Steps

Create an ordered checklist where each step:
- Can be independently committed
- Is described with enough specificity to estimate and review
- Follows this rough ordering:
  1. Data model / schema changes first
  2. Backend logic / service layer second
  3. API / interface layer third
  4. Frontend / consumer changes fourth
  5. Tests last (unit, then integration)

Flag steps with high uncertainty or unknown dependencies.

### Step 4 — List Affected Files / Components

Based on the technical approach, list every file or component expected to change:
- Type of change: new / modify / delete
- Brief description of what changes

If the project context does not provide enough information about the codebase structure, note this as a gap and ask the developer to fill it in during implementation.

### Step 5 — List Integration Points and Dependencies

For each external dependency or integration point:
- What it is (internal service, external API, database, config)
- How this issue interacts with it
- Any known risks or constraints

### Step 6 — List Business Rules to Enforce

Pull business rules directly from the SPEC FEAT section. These are non-negotiable implementation constraints that must be verified in code review. If none are explicitly stated, flag this as a gap.

### Step 7 — Generate Backend Story Stub

Create a pre-filled `templates/backend_story.md` with:
- Metadata linked to this issue and SPEC
- Description matching the issue's user story
- Business rules from the SPEC
- Blank sections for: endpoints, request/response, DB changes, acceptance criteria

Save to: `projects/<name>/docs/stories/YYYY-MM-DD-backend-[issue-slug].md`

### Step 8 — Generate QA Story Stub

Create a pre-filled `templates/qa_story.md` with:
- Metadata linked to this issue and SPEC
- Description of what is being tested
- Preconditions derived from issue dependencies and acceptance criteria
- Blank test scenarios (one stub per acceptance criterion)

Save to: `projects/<name>/docs/stories/YYYY-MM-DD-qa-[issue-slug].md`

---

## Output

Use `templates/dev_plan.md` as the document structure.

Save to: `projects/<name>/docs/issues/YYYY-MM-DD-[issue-slug]-devplan.md`

Update the issue file's Linked Documents section with paths to the new dev plan, backend story stub, and QA story stub.

Present all three documents to the user before saving.

---

## Quality Check Before Saving

- [ ] Technical approach explains the core mechanism in plain language
- [ ] Every acceptance criterion from the issue maps to at least one implementation step
- [ ] Business rules section is not empty (either rules listed or gap flagged)
- [ ] Backend story stub created and linked
- [ ] QA story stub created and linked
- [ ] Open risks identified (at least one entry, or explicitly state "none identified")

---

## Rules

- Development plans describe **how** — they do not restate the **what** (that is in the issue and SPEC)
- Effort estimates are in hours, not story points — be concrete
- If technical decisions depend on unresolved SPEC TBDs, flag those items as blocked rather than guessing
- Never fabricate stack or architecture details not present in project context
- The backend story and QA story stubs are starting points — developers and QA fill in the details
