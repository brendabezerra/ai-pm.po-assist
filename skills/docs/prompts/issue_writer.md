# Issue Writer Prompt

## Purpose

Break a completed SPEC into discrete, actionable issues — atomic units of work that a developer can pick up and implement independently. Each issue maps to one SPEC feature section. Output is a set of populated issue files plus a summary table for sprint planning.

---

## Inputs Required

1. **SPEC file** — path to `projects/<name>/docs/specs/YYYY-MM-DD-feature.md`
2. **Project context** — `projects/<name>/context.md` (team, sprint, priorities)
3. **Sprint capacity** (optional) — if provided, use to flag issues that may not fit the current sprint

---

## Generation Steps

### Step 1 — Read the SPEC

Extract:
- All FEAT sections (FEAT-01, FEAT-02, ...)
- Data requirements (may generate a dedicated data/migration issue)
- Interface specifications (may generate a dedicated integration issue)
- Dependencies between features
- Open questions (flag issues that depend on unresolved TBDs)

### Step 2 — Determine Issue Granularity

A good issue is:
- **Independently implementable** — a developer can start and finish it without waiting for another issue to be done (except declared dependencies)
- **Testable** — QA can verify completion against acceptance criteria
- **Sized S–XL** — if an issue would be XL+, split it further

Splitting rules:
- Split by user role (admin vs. end user flows)
- Split by read vs. write (fetch data separately from save data)
- Split by layer if needed (backend API separately from frontend UI)
- Keep data migration as a separate issue
- Keep external integrations as a separate issue

### Step 3 — Write Each Issue

For each issue, populate `templates/issue.md`:

- **Title**: Active verb phrase — "Add [X]", "Implement [Y]", "Update [Z]"
- **Description**: User story format — "As [user], I want [action], so that [benefit]"
- **Acceptance criteria**: Derived directly from the SPEC's FEAT acceptance criteria. One criterion per testable condition.
- **Definition of done**: Use the standard DoD checklist from the template
- **Dependencies**: List other issues this one blocks or is blocked by. Reference by issue title or ID.
- **Size estimate**: S (< 4h) / M (4–8h) / L (1–3 days) / XL (3+ days)
- **Priority**: Match PRD requirement priority (P1/P2/P3)
- **Parent SPEC feature**: Reference the FEAT-XX section

### Step 4 — Suggest Sprint Ordering

Based on dependencies, propose an order:
1. Foundation issues first (data model, migrations, API contracts)
2. Independent issues next (features with no blocking dependencies)
3. Integration issues last (features that depend on multiple completed issues)

Flag issues that should NOT be in the same sprint if they have hard dependencies.

### Step 5 — Flag TBD-Dependent Issues

If a SPEC has open questions (TBDs), identify which issues are blocked by those TBDs and mark them as `status: blocked` with a note explaining what decision is needed.

---

## Output

### Issue Files

Save each issue to: `projects/<name>/docs/issues/YYYY-MM-DD-[issue-slug].md`

Use today's date for all files.

### Summary Table (shown to user)

| Issue ID | Title | SPEC Feature | Size | Priority | Sprint | Depends On | Status |
|---|---|---|---|---|---|---|---|
| ISSUE-01 | | FEAT-01 | S/M/L/XL | P1/P2/P3 | | | open/blocked |

### Sprint Ordering Recommendation

State the suggested implementation order as a numbered list with brief rationale for each dependency.

---

## Rules

- Every SPEC FEAT section must produce at least one issue
- Every issue must have at least one acceptance criterion
- Do not include implementation details in issues — those belong in the dev plan
- If a FEAT section has an unresolved TBD, create the issue anyway but mark it blocked and add the open question as a note
- Size estimates are approximate — flag when high uncertainty exists
- Always present the summary table to the user for review before saving issue files
