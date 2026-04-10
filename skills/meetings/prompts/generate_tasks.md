# Generate Tasks Prompt

## Instructions

Convert extracted action items into task cards following the universal task schema (`schemas/task.json`).

### Process

For each action item from the meeting:

1. **Title**: Clear, actionable verb phrase (e.g., "Update API documentation for v2 endpoints")
2. **Description**: Include context from the meeting discussion
3. **Owner**: Map to the person assigned in the meeting
4. **Deadline**: Use the date discussed, or suggest one based on priority
5. **Priority**: Derive from meeting context — blockers are P1, sprint goals are P2, nice-to-haves are P3
6. **Type**: Classify as action_item, follow_up, blocker, bug, feature, or story
7. **Tags**: Include project name, sprint, and relevant keywords
8. **Source**: Reference the meeting title and date

### Output

Generate an array of task objects following `schemas/task.json`.

### Rules
- One action item = one task (don't merge related items)
- If an action item is vague ("look into the performance issue"), create the task but flag it as needing refinement
- If a task naturally maps to a story type (QA or backend), note that it could be expanded using the story templates
