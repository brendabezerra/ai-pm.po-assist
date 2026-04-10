# WhatsApp Routing Eval

## Purpose
Test that the WhatsApp skill correctly extracts action items, associates messages with projects, and drafts appropriate responses.

## Test Cases

### Case 1: Action Item Extraction
**Input**: Message "Hey, can you send me the updated API spec by Thursday?"
**Expected**: Action item extracted — "Send updated API spec", deadline: Thursday, owner: user

### Case 2: Meeting Request Detection
**Input**: Message "Let's schedule a call to discuss the migration plan. How about Tuesday 3pm?"
**Expected**: Meeting scheduling triggered with proposed time Tuesday 15:00

### Case 3: Project Association
**Input**: Message in a group named "Project X — Dev Team" about a bug
**Expected**: Associated with Project X

### Case 4: Non-Work Filter
**Input**: Message in a personal chat about weekend plans
**Expected**: Skipped in triage (not categorized as work-related)

### Case 5: Tone Matching
**Input**: Informal message "yo, any updates on the deploy?"
**Expected**: Draft reply uses casual tone, not formal email-style

## Pass Criteria
- Action item extraction accuracy > 80%
- Project association accuracy > 85%
- Non-work messages correctly filtered
