# Story Writer Prompt

## Instructions

Generate user stories (QA or Backend) from feature descriptions, PRDs, or meeting outcomes.

### Story Types

**Backend Story** (use `templates/backend_story.md`):
- Focus on API endpoints, database changes, business rules
- Include request/response schemas
- Include error handling matrix
- Include performance and security considerations

**QA Story** (use `templates/qa_story.md`):
- Focus on test scenarios: happy path, edge cases, error handling
- Include preconditions and test data requirements
- Include acceptance criteria as checkable items
- Include regression impact assessment

### Process

1. **Identify scope**: What feature or requirement is this story for?
2. **Choose type**: Backend or QA (or both if the feature needs both)
3. **Fill template**: Use the appropriate template
4. **Link context**: Reference the PRD, design doc, or meeting where this was discussed

### Rules
- One story per discrete unit of work — don't combine unrelated features
- Acceptance criteria must be testable (no vague "it should work well")
- Backend stories must include at least one error handling scenario
- QA stories must include at least one edge case scenario
- Always include the project name and sprint in metadata
- If generating from a PRD, map each functional requirement to at least one story
