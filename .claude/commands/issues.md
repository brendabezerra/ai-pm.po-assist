# /issues — Break SPEC into Issues

## What This Command Does

Takes a completed SPEC and breaks it into discrete, independently implementable issues. Each issue maps to one SPEC feature section and is sized, prioritized, and ordered for sprint planning. Outputs one issue file per issue plus a summary table.

This covers step 6 of the PO workflow: **break SPEC into issues**.

---

## When to Use

- After SPEC is approved (status = `approved`)
- Before sprint planning to prepare the issue backlog
- When a SPEC is updated and new issues need to be generated

---

## How to Run

```
/issues
```

The agent will ask:
1. Which project?
2. Path to SPEC file (e.g., `projects/<name>/docs/specs/2026-04-10-feature.md`)
3. Sprint capacity? (optional — used to flag issues that may not fit the current sprint)

---

## Execution Steps

1. **Verify SPEC status** — if draft, ask user to confirm it is ready before proceeding
2. **Read the SPEC** — extract all FEAT sections, data requirements, interface specifications, open questions
3. **Read project context** — `projects/<name>/context.md` (team, sprint, priorities)
4. **Run** `skills/docs/prompts/issue_writer.md`
5. **Present** the summary table to the user for review
6. **Confirm** issue list, sizes, priorities, and sprint ordering with user
7. **Save** each issue file to `projects/<name>/docs/issues/YYYY-MM-DD-[issue-slug].md` after user approval

---

## Output Structure

### Summary Table (shown first, before saving)

| Issue ID | Title | SPEC Feature | Size | Priority | Sprint | Depends On | Status |
|---|---|---|---|---|---|---|---|
| ISSUE-01 | | FEAT-01 | S/M/L/XL | P1/P2/P3 | | | open/blocked |

### Sprint Ordering Recommendation

Numbered list of suggested implementation order with dependency rationale.

### Issue Files

Each file uses `templates/issue.md`. Saved to `projects/<name>/docs/issues/`.

---

## Issue File Contents (per issue)

- **Title** — actionable verb phrase
- **Description** — user story (As / I want / So that)
- **Acceptance Criteria** — from SPEC FEAT section, one per testable condition
- **Definition of Done** — standard DoD checklist
- **Dependencies** — blocks / blocked by
- **Size** — S / M / L / XL
- **Priority** — P1 / P2 / P3
- **Parent SPEC section** — FEAT-XX reference

---

## Next Steps After This Command

| Status | Next Step |
|---|---|
| Issues approved | `/devplan` for each issue (in dependency order) |
| Blocked issues exist | Resolve SPEC TBDs first |
| Sprint capacity exceeded | Negotiate scope with stakeholders |

---

## Guardrails

- Every SPEC FEAT must produce at least one issue — do not skip features
- Issues blocked by unresolved SPEC TBDs are created but marked `status: blocked`
- Do not include implementation details in issues — that belongs in dev plans
- Present summary table before saving any files
- Save location: `projects/<name>/docs/issues/`
