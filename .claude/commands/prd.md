# /prd — Generate PRD

You are generating a Product Requirements Document. Follow the documentation flow in `workflows/documentation_flow.md`.

## Instructions

1. Read `rules/agent_rules.md` for behavioral guidelines.
2. Determine context:
   - **Which project?** If not specified, ask.
   - Read the project's context file from `projects/<name>/context.md`
3. Gather input:
   - If the user provided a feature description, use it
   - If the user references a meeting, check for meeting notes
   - If the user says "from the last meeting", find the most recent meeting notes for that project

4. Generate the PRD:
   - Use `templates/prd.md` as the structure
   - Apply `skills/docs/prompts/prd.md` for section guidelines
   - Fill every section with available information
   - Mark missing information as "[TBD — needs input]"
   - List questions that need answers before the PRD is complete

5. Present for review:
   - Show the complete PRD to the user
   - Ask if they want to edit, approve, or provide more input
   - Once approved, save to `projects/<name>/docs/prds/[date]-[feature].md`

## Arguments
- `/prd` — interactive, will ask for feature and project
- `/prd [feature description]` — generate from description, will ask for project if ambiguous

## Output
Complete PRD following the template structure, with clear TBD markers for any missing information.
