# Document Quality Eval

## Purpose
Test that the docs skill generates complete, well-structured documents that follow templates correctly.

## Test Cases

### Case 1: PRD Completeness
**Input**: Feature request with clear requirements
**Expected**: All template sections filled. No required section left blank (except those legitimately TBD).

### Case 2: PRD with Missing Info
**Input**: Vague feature request "We need better search"
**Expected**: Problem statement filled, but Timeline, Requirements, and Metrics marked as "[TBD — needs input]" with clarifying questions listed

### Case 3: Design Doc Alternatives
**Input**: Technical design for a new service
**Expected**: "Alternatives Considered" section has at least 2 alternatives with pros/cons

### Case 4: Backend Story Completeness
**Input**: Feature from a PRD requirement
**Expected**: Endpoints defined, request/response schemas included, at least 1 error scenario, acceptance criteria present

### Case 5: QA Story Test Coverage
**Input**: Feature description
**Expected**: Happy path, at least 1 edge case, at least 1 error handling scenario, preconditions listed

### Case 6: Template Adherence
**Input**: Any document generation request
**Expected**: Output structure matches the template exactly — no missing headers, no extra sections

## Pass Criteria
- Template adherence: 100% (all required sections present)
- TBD sections correctly identified when input is insufficient
- No fabricated requirements or test cases
- Acceptance criteria are testable (not vague)
