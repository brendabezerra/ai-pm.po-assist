# /analyze — Requirements Analysis

## What This Command Does

Takes a set of requirements from a stakeholder session and analyzes them against the current project scope, existing PRDs, and known business rules. Surfaces conflicts, missing rules, scope gaps, and risks before you write the PRD.

This covers steps 2–3 of the PO workflow: **cross requirements with scope** and **analyze changes vs. what exists**.

---

## When to Use

- After a requirements gathering session (run `/followup` first to extract raw requirements)
- Before starting a new PRD to validate the input
- When evaluating a change request against an existing feature

---

## How to Run

```
/analyze
```

The agent will ask:
1. Which project? (or pass project name directly)
2. Path to requirements file — or paste requirements as raw text

---

## Execution Steps

1. **Load project context** from `projects/<name>/context.md`
2. **Load existing PRDs** from `projects/<name>/docs/prds/` (if any)
3. **Run** `skills/docs/prompts/requirements_analysis.md` against the requirements and context
4. **Output** the analysis — do not proceed until the user reviews it
5. **Ask** the user: "Do you want to proceed to PRD with these requirements?"
   - Yes → suggest running `/prd`
   - No → list what needs to be resolved first

---

## Output Structure

### 1. Requirements Classification Table
Each requirement classified as: New / Change / Conflict / Duplicate / Out of scope

### 2. Business Rule Conflicts
Any new requirement that contradicts or is incompatible with existing rules. Cites source document and section.

### 3. Missing Business Rules
Requirements that are under-specified — edge cases not governed by any stated rule.

### 4. Risk Assessment Table
Requirement / Risk / Probability / Impact / Mitigation

### 5. Recommendation
- Ready to proceed to PRD: **Yes / No / Conditional**
- If conditional: list what must be resolved first

---

## Next Steps After This Command

| Decision | Next Step |
|---|---|
| Requirements are clean | `/prd` |
| Conflicts found | Resolve with stakeholders, re-run `/analyze` |
| Missing rules | Add rules to requirements file, re-run `/analyze` |
| Out of scope items | Confirm scope change with stakeholders first |

---

## Guardrails

- Never fabricate existing business rules — only cite rules from existing project documents
- Never mark requirements as "out of scope" without citing the scope boundary from context.md
- Always present the full analysis before suggesting next steps
- Do not generate a PRD automatically after analysis — wait for explicit user confirmation
