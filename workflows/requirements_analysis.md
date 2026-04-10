# Requirements Analysis Workflow

## Overview

How raw stakeholder requirements become a validated, scope-checked, risk-assessed input ready for PRD writing. Covers steps 1–3 of the PO workflow.

---

## Steps

```
Stakeholder Session
        ↓
  /followup — extract raw requirements from meeting notes
        ↓
  Fill requirements template
        ↓
  /analyze — scope check + business rule analysis + risk assessment
        ↓
  Resolve conflicts and gaps (if any)
        ↓
  Requirements sign-off → ready for /prd
```

---

## Step 1 — Capture Requirements (Stakeholder Session)

**Trigger:** Meeting with stakeholders where requirements are discussed.

**Action:**
1. Take raw notes during the meeting
2. Run `/followup` with the meeting notes
3. The meetings skill extracts: decisions, action items, new feature requests, constraints

**Output:** Structured meeting notes + raw list of requirements

**Template:** `templates/requirements.md`

**Save to:** `projects/<name>/docs/requirements/YYYY-MM-DD-[feature].md`

---

## Step 2 — Structure Requirements

**Trigger:** After `/followup` completes.

**Action:**
1. Open the requirements template
2. For each extracted requirement:
   - Assign a REQ-XX ID
   - Note the requester and business justification
   - Define an acceptance condition (what does "done" look like for this requirement?)
   - Assign initial priority (P1/P2/P3)
3. List anything that was explicitly out of scope

**Tip:** If a requirement has no business justification, flag it as an open question — don't carry forward unsupported requirements.

---

## Step 3 — Analyze Requirements Against Scope and Existing System

**Trigger:** Requirements file is complete.

**Action:** Run `/analyze`

**The agent will:**
1. Load `projects/<name>/context.md` (current scope, goals, team)
2. Load existing PRDs from `projects/<name>/docs/prds/`
3. Classify each requirement: New / Change / Conflict / Duplicate / Out of scope
4. Identify business rule conflicts (requirement vs. existing rule)
5. Identify missing rules (requirement doesn't specify governing edge cases)
6. Produce a risk assessment table
7. State a recommendation: Ready / Conditional / Not ready

**Output:** Analysis document with classification table, conflict table, missing rules, risk table, and recommendation.

---

## Step 4 — Resolve Conflicts and Gaps

**Trigger:** `/analyze` output shows conflicts, missing rules, or a Conditional recommendation.

**For each conflict:**
- Schedule a follow-up with the relevant stakeholder
- Update the requirements file with the resolution
- Reference the resolution in the conflict entry

**For each missing rule:**
- Define the rule with the product owner / business stakeholder
- Add the rule to the requirements file
- Reference it in the SPEC later

**For out-of-scope items:**
- Confirm with stakeholders whether scope should change
- If yes: update `projects/<name>/context.md` before proceeding
- If no: remove the requirement from the file

**Re-run `/analyze` after resolving issues** to confirm the recommendation changes to "Ready."

---

## Step 5 — Sign Off and Proceed

**Trigger:** `/analyze` recommendation is "Ready to proceed to PRD."

**Confirm:**
- [ ] All REQ-XX items classified (no "Unknown" entries)
- [ ] Zero unresolved conflicts
- [ ] All missing rules added
- [ ] Open questions in requirements file answered or moved to PRD Open Questions
- [ ] Stakeholder who raised requirements has confirmed

**Next Step:** `/prd`

---

## Data Flow

| Input | Source | Output | Destination |
|---|---|---|---|
| Meeting notes | `/followup` | Requirements file | `projects/<name>/docs/requirements/` |
| Requirements file + context | `/analyze` | Analysis document | Presented to user (not saved) |
| Resolved requirements | PM + stakeholders | Updated requirements file | `projects/<name>/docs/requirements/` |

---

## Dependencies

- **Google Workspace MCP** (optional) — for pulling email context on requirements
- **Project context file** — must exist before `/analyze` runs
- **Existing PRDs** — used for conflict detection (missing is OK if no prior PRDs exist)

---

## Output Quality Check

Before moving to `/prd`, verify:
- [ ] Every REQ-XX has a business justification (not just a feature request)
- [ ] Every REQ-XX has an acceptance condition
- [ ] No unresolved conflicts
- [ ] Risk table reviewed and any P1 risks have mitigation plans
- [ ] Requirements file status updated to `reviewed`
