# Meeting Extraction Eval

## Purpose
Test that the meetings skill correctly extracts decisions, action items, and blockers from raw meeting notes.

## Test Cases

### Case 1: Explicit Action Item
**Input**: "John will update the API documentation by Friday."
**Expected**: Action: "Update API documentation", Owner: John, Deadline: Friday

### Case 2: Implicit Action Item
**Input**: "We need to figure out the auth flow before moving forward."
**Expected**: Action: "Define auth flow", Owner: TBD, Priority: P1 (blocker implied)

### Case 3: Decision Extraction
**Input**: "After discussing both options, we decided to go with PostgreSQL instead of MongoDB because of the relational data requirements."
**Expected**: Decision: "Use PostgreSQL over MongoDB", Rationale: "Relational data requirements"

### Case 4: Blocker Extraction
**Input**: "We can't proceed with the integration until the DevOps team provides the staging credentials."
**Expected**: Blocker: "Waiting for staging credentials from DevOps", Impact: "Integration blocked"

### Case 5: Ambiguous Notes
**Input**: "Talked about performance. Need to look into it."
**Expected**: Action flagged as ambiguous — "Investigate performance issue", Owner: TBD, note: "Needs clarification — vague notes"

### Case 6: Multiple Items in One Paragraph
**Input**: "Maria will handle the frontend changes, Pedro takes the backend, and we need QA to start writing test cases by next sprint."
**Expected**: 3 separate action items with correct owners

## Pass Criteria
- Explicit action items: 100% extraction rate
- Decision extraction with rationale: > 90%
- No fabricated items (zero false positives)
- Ambiguous notes correctly flagged rather than guessed
