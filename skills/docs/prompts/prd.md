# PRD Generation Prompt

## Instructions

Generate a Product Requirements Document using the template at `templates/prd.md`.

### Process

1. **Gather context**: Read the project context file and any provided input (meeting notes, feature description, stakeholder request)
2. **Fill template**: Populate every section of the PRD template
3. **Mark unknowns**: Clearly label sections where information is missing as "[TBD — needs input]"
4. **Save**: Output as a markdown file in the project directory

### Section Guidelines

- **Problem Statement**: Focus on the user pain point, not the solution. Include data if available.
- **Goals & Success Metrics**: Each goal must have a measurable metric and target value.
- **User Stories**: Write from the user's perspective. Cover primary, secondary, and edge cases.
- **Scope**: Be explicit about what's out of scope to prevent scope creep.
- **Requirements**: Separate functional from non-functional. Assign priorities.
- **Timeline**: Break into phases if the feature is large.
- **Risks**: Include technical, business, and user adoption risks.

### Rules
- Never fabricate requirements that weren't provided — mark as TBD
- If the input is too vague to generate a meaningful PRD, list what information is needed before proceeding
- Cross-reference with existing project goals to ensure alignment
- Use the project's terminology and conventions
