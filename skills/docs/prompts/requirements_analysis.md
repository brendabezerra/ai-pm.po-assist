# Requirements Analysis Prompt

## Purpose

Analyze a set of raw requirements against the current project scope and existing system. Produce a structured analysis that surfaces what changes, what conflicts, what is missing, and what risks need to be addressed before writing a PRD.

---

## Inputs Required

1. **Requirements file** — path to `projects/<name>/docs/requirements/YYYY-MM-DD-feature.md` or raw requirements text
2. **Project context** — `projects/<name>/context.md` (goals, scope, team, sprint)
3. **Existing PRDs** (if any) — paths to relevant files under `projects/<name>/docs/prds/`

If any input is missing, ask the user before proceeding. Do not fabricate context.

---

## Analysis Steps

### Step 1 — Load Context

Read:
- `projects/<name>/context.md` — what the project does today, its goals, current scope boundaries
- Any referenced existing PRDs — what requirements already exist and are in scope

### Step 2 — Classify Each Requirement

For each requirement in the input, classify it as one of:

| Class | Meaning |
|---|---|
| **New** | Does not exist in current scope — adds capability |
| **Change** | Modifies existing behavior — updates a current capability |
| **Conflict** | Contradicts or is incompatible with existing rules, goals, or requirements |
| **Duplicate** | Already covered by an existing requirement |
| **Out of scope** | Explicitly outside the project boundary as defined in context.md |

### Step 3 — Identify Business Rule Conflicts

Review the requirements against:
- Business rules stated in existing PRDs
- Goals defined in `context.md`
- Acceptance criteria of any active sprint

Flag any requirement that:
- Contradicts an existing business rule (state which rule and why)
- Creates an ambiguous state (two requirements that could both apply in the same scenario)
- Removes a constraint that another requirement depends on

### Step 4 — Identify Missing Rules

Look for requirements that are stated at a high level but are missing the rule that governs edge cases. Flag each gap:

- What behavior is unspecified?
- In what scenario does this matter?
- What rule should be defined to resolve it?

### Step 5 — Assess Risk

For each New or Change requirement, assess:

| Dimension | Question |
|---|---|
| **Impact** | How much of the existing system does this touch? |
| **Dependency** | Does it depend on something not yet built or confirmed? |
| **Reversibility** | Can this be rolled back easily if it fails? |
| **Timeline risk** | Is there a hard deadline attached? |

---

## Output Format

### Requirements Classification

| REQ # | Requirement | Class | Notes |
|---|---|---|---|
| REQ-01 | | New / Change / Conflict / Duplicate / Out of scope | |

### Business Rule Conflicts

| Conflict | Existing Rule | New Requirement | Impact |
|---|---|---|---|
| | | | |

> If none: state "No conflicts identified."

### Missing Business Rules

| Gap | Scenario | Rule Needed |
|---|---|---|
| | | |

> If none: state "No missing rules identified."

### Risk Assessment

| REQ # | Risk | Probability | Impact | Mitigation |
|---|---|---|---|---|
| | | High / Medium / Low | High / Medium / Low | |

### Recommendation

State clearly:
- Is this set of requirements ready to proceed to PRD? **Yes / No / Conditional**
- If conditional: what must be resolved first (list open questions or missing rules)
- Suggested adjustments to scope or priority before PRD writing

---

## Rules

- Never fabricate existing business rules — only cite rules explicitly stated in existing documents
- If project context is missing or incomplete, ask the user to fill it in before proceeding
- Mark every conflict with the source document and section it was found in
- Do not make recommendations outside the scope of the provided documents
- If a requirement is ambiguous, flag it with a clarifying question rather than assuming intent
