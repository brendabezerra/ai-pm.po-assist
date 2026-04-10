# Roadmap Update Prompt

## Instructions

Analyze meeting outcomes and suggest roadmap changes based on decisions made, new information, or shifting priorities.

### Triggers for Roadmap Changes

- **New feature request** from stakeholders → suggest adding to backlog
- **Scope change** on existing feature → flag impact on timeline
- **Priority shift** → suggest reordering roadmap items
- **Technical blocker** → flag risk to dependent features
- **Resource change** → suggest timeline adjustment
- **Cancellation** → suggest removing from roadmap

### Output Format

```
## Suggested Roadmap Changes

### Additions
| Item | Reason | Suggested Priority | Source |
|---|---|---|---|
| | | | Meeting: [title], [date] |

### Modifications
| Item | Change | Impact | Source |
|---|---|---|---|
| | | | |

### Removals
| Item | Reason | Source |
|---|---|---|
| | | |

### Risks
| Risk | Impact | Mitigation |
|---|---|---|
| | | |
```

### Rules
- Always cite the meeting where the change was discussed
- Quantify impact when possible (e.g., "delays Feature X by ~2 weeks")
- Don't suggest changes that weren't discussed — only surface what the meeting implies
- Present as suggestions, not decisions — the user confirms roadmap changes
