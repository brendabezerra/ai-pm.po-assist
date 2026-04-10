# Extract Action Items Prompt

## Instructions

Given raw meeting notes, extract all action items, decisions, and blockers into a structured format.

### Extraction Rules

**Action Items** — look for:
- Explicit assignments: "John will...", "Maria to...", "[Name] takes ownership of..."
- Commitments: "We agreed to...", "Next step is...", "By Friday we need..."
- Requests: "Can you...?", "Please...", "We need someone to..."
- Implicit tasks: anything that implies work to be done, even if not explicitly assigned

**Decisions** — look for:
- "We decided...", "The decision is...", "We're going with..."
- Consensus moments: "Everyone agreed...", "The team chose..."
- Rejections: "We will NOT do...", "Option B was rejected because..."

**Blockers** — look for:
- "We're blocked on...", "Can't proceed until...", "Waiting for..."
- Dependencies on external teams or approvals
- Missing information or resources

### Output Format

Follow the `schemas/action_items.json` schema. For each item:
- Every action item MUST have an owner. If unclear, mark as "TBD — needs assignment"
- Every action item SHOULD have a deadline. If not discussed, mark as "TBD — needs deadline"
- Decisions must include rationale when discussed
- Blockers must include impact description

### Rules
- Don't invent action items that weren't discussed
- If notes are ambiguous, flag the ambiguity rather than guessing
- Group items by topic/theme when possible
- Cross-reference attendees with project team members for full names
