# SPEC Generation Prompt

## Purpose

Transform a completed, approved PRD into a Functional Specification (SPEC). The SPEC is the bridge between the PRD (what and why) and the development work (how). It defines every feature in sufficient detail that a developer or QA engineer can work from it without needing to interpret intent.

---

## Inputs Required

1. **PRD file** — path to `projects/<name>/docs/prds/YYYY-MM-DD-feature.md`
2. **Project context** — `projects/<name>/context.md`
3. **Requirements file** (optional) — if available, use for additional detail and accepted conditions

If the PRD is in draft status, ask the user to confirm it is approved before generating the SPEC.

---

## Generation Steps

### Step 1 — Read the PRD

Extract:
- All functional requirements (from the Requirements section)
- All user stories
- Scope boundaries (in scope / out of scope)
- Goals and success metrics (to validate acceptance criteria)
- Timeline and phasing (to understand if the SPEC covers all phases or one phase)
- Risks (to surface as edge cases in the SPEC)

### Step 2 — Map PRD Requirements to SPEC Features

Create one FEAT section per distinct functional requirement or user story group. Assign IDs (FEAT-01, FEAT-02, ...) that match the PRD requirement IDs where possible.

### Step 3 — Expand Each Feature

For each FEAT section, define:

1. **Description** — what the feature does from the user's perspective, in plain language
2. **User Flow** — step-by-step sequence of events (numbered list)
3. **Business Rules** — explicit rules the implementation must enforce. If none are stated in the PRD, derive them from the description and flag as `[derived — confirm with PM]`
4. **Acceptance Criteria** — Given/When/Then format, one per testable condition. Must be specific enough to write a QA test case from.
5. **Edge Cases** — what happens in boundary or failure scenarios. For each: describe the trigger and the expected system behavior.
6. **Out of scope** — what is explicitly excluded from this feature's implementation

### Step 4 — Define Data Requirements

List all data fields the feature reads, writes, or depends on. For each:
- Field name
- Type
- Source (user input / system-generated / external API / database)
- Validation rules
- Notes

### Step 5 — Define Interface Specifications

For each system boundary the feature crosses (API, service, external integration):
- Input and output contracts at a functional level (not implementation level)
- Error states and how the system handles them
- Constraints (rate limits, size limits, required fields)

### Step 6 — Enumerate Error States

Build a complete table of error states across all features:
- What triggers the error
- What the system does
- What the user sees (message or behavior)

### Step 7 — Mark TBDs

Wherever the PRD does not provide enough information to write a complete SPEC section, write `TBD` and add an open question entry at the bottom of the SPEC.

---

## Output

Use `templates/spec.md` as the document structure.

Save to: `projects/<name>/docs/specs/YYYY-MM-DD-[feature-name].md`

Present the full SPEC to the user for review before saving. Ask the user to confirm or edit any `[derived — confirm with PM]` items and all TBDs.

---

## Quality Check Before Saving

Before presenting the SPEC to the user, verify:

- [ ] Every PRD functional requirement maps to at least one FEAT section
- [ ] Every FEAT section has at least one Given/When/Then acceptance criterion
- [ ] Every FEAT section has at least one edge case
- [ ] No fabricated business rules (all rules either cited from PRD or flagged as derived)
- [ ] All TBDs are listed in Open Questions with a clear question for the PM
- [ ] Status is set to `draft`

---

## Rules

- One SPEC per PRD — do not combine multiple PRDs into one SPEC
- The SPEC defines **what** in detail — it does not specify **how** (that is the design doc's job)
- Acceptance criteria must be testable — if you cannot write a test case from it, it is not specific enough
- If the PRD has phases, ask the PM whether the SPEC should cover all phases or one phase at a time
- Never remove scope from the PRD — if you disagree with scope, add an open question
