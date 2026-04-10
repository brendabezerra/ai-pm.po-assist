# Design Document Generation Prompt

## Instructions

Generate a Design Document using the template at `templates/design_doc.md`.

### Process

1. **Read PRD**: If a PRD exists for this feature, read it first for requirements context
2. **Gather technical input**: From meeting notes, technical discussions, or user input
3. **Fill template**: Populate all sections of the design doc template
4. **Mark unknowns**: Label sections needing more investigation as "[TBD — needs investigation]"

### Section Guidelines

- **Context**: Link to the PRD and explain why this design is needed now
- **Current State**: Describe what exists today — don't skip this even for greenfield features
- **Proposed Design**: Be specific about components, interfaces, and data flow
- **Alternatives Considered**: Always include at least 2 alternatives with clear trade-offs
- **Security**: Consider auth, data privacy, and compliance implications
- **Testing Strategy**: Include unit, integration, and E2E test plans
- **Rollout Plan**: Include rollback strategy for each phase

### Rules
- Never skip the "Alternatives Considered" section — it demonstrates rigor
- Mark assumptions clearly and separately from confirmed decisions
- If the design requires decisions from other teams, list them as open questions
- Reference the project's tech stack and architecture conventions
