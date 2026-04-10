# /spec — Generate Functional Specification

## What This Command Does

Transforms a completed, approved PRD into a Functional Specification (SPEC). The SPEC bridges the PRD (what and why) and the development work (how). It defines every feature in enough detail that developers and QA engineers can work from it without interpreting intent.

This covers step 5 of the PO workflow: **create SPEC from PRD**.

---

## When to Use

- After a PRD is approved (status = `approved`)
- Before breaking work into issues
- When a PRD change requires the SPEC to be updated

---

## How to Run

```
/spec
```

The agent will ask:
1. Which project?
2. Path to PRD file (e.g., `projects/<name>/docs/prds/2026-04-10-feature.md`)
3. Does the SPEC cover all PRD phases, or one specific phase?

---

## Execution Steps

1. **Verify PRD status** — if draft, ask user to confirm it is ready before proceeding
2. **Read the PRD** — extract functional requirements, user stories, scope, risks
3. **Read project context** — `projects/<name>/context.md`
4. **Run** `skills/docs/prompts/spec.md`
5. **Quality check** — verify all PRD requirements are covered, all acceptance criteria are testable, all TBDs are in Open Questions
6. **Present** the full SPEC to the user for review
7. **Confirm** any `[derived — confirm with PM]` items and TBDs with the user
8. **Save** to `projects/<name>/docs/specs/YYYY-MM-DD-[feature-name].md` after user approval

---

## Output Structure

The SPEC uses `templates/spec.md`:

- **Metadata** — project, author, status (draft), links to PRD and requirements
- **Purpose** — what the SPEC covers
- **Scope** — in / out
- **Features** — one FEAT-XX section per PRD functional requirement
  - Description, User Flow, Business Rules, Acceptance Criteria, Edge Cases
- **Data Requirements** — all fields the feature reads/writes
- **Interface Specifications** — API/integration contracts at functional level
- **Error States** — complete table of failure scenarios
- **Open Questions** — all TBDs with clarifying questions

---

## Next Steps After This Command

| Status | Next Step |
|---|---|
| SPEC approved | `/issues` |
| TBDs remain | Resolve open questions, update SPEC |
| Scope changed during review | Update PRD first, then regenerate SPEC |

---

## Guardrails

- Only run on approved PRDs — do not generate SPEC from a draft PRD without user confirmation
- Every FEAT section must trace back to a PRD requirement — do not invent features
- Never fabricate business rules — derive from PRD only, and flag derived rules for PM confirmation
- Present for review before saving
- Save location: `projects/<name>/docs/specs/`
