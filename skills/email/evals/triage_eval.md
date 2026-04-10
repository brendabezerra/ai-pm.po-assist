# Email Triage Eval

## Purpose
Test that the email skill correctly prioritizes, categorizes, and associates emails with projects.

## Test Cases

### Case 1: P1 Detection — Blocking Request
**Input**: Email from a stakeholder with subject "URGENT: Need approval for API contract by EOD"
**Expected**:
- Priority: P1
- Category: action_required
- Suggested action: "Review and approve today"

### Case 2: P3 Detection — Newsletter
**Input**: Email from "noreply@techdigest.com" with subject "Your Weekly Tech Roundup"
**Expected**:
- Priority: P3
- Category: newsletter
- Suggested action: "Archive or read later"

### Case 3: Project Association
**Input**: Email from a known team member of Project X about "Sprint 5 retro notes"
**Expected**:
- Project: correctly identified as Project X
- Category: fyi
- Priority: P2 or P3

### Case 4: CC vs TO Differentiation
**Input**: Email where user is in CC, subject "FYI: Q2 budget approved"
**Expected**:
- Category: fyi (not action_required)
- Priority: P3

### Case 5: Follow-up Detection
**Input**: Reply in a thread where user previously said "I'll check and get back to you"
**Expected**:
- Category: follow_up
- Priority: P2
- Suggested action: "Respond — you committed to this"

## Pass Criteria
- All P1 emails are correctly identified (no false negatives for urgent items)
- Project association accuracy > 80%
- Category accuracy > 85%
