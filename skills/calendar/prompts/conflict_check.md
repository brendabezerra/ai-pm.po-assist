# Conflict Check Prompt

## Instructions

Analyze the given calendar events and identify scheduling conflicts.

### Conflict Types

| Type | Description | Severity |
|---|---|---|
| **Hard conflict** | Two events at the exact same time | High — must resolve |
| **Buffer conflict** | Back-to-back meetings with no break | Medium — suggest buffer |
| **Travel conflict** | Two in-person events at different locations without travel time | High — must resolve |
| **Overload** | 5+ hours of meetings in a single day | Medium — flag for awareness |

### Output Format

For each conflict found:
- **Events**: [Event A] vs [Event B]
- **Type**: Hard / Buffer / Travel / Overload
- **Suggestion**: Which to keep, reschedule, or decline

### Rules
- Back-to-back means less than 10 minutes between end of one and start of another
- Overload threshold: more than 5 hours of scheduled meetings in one day
- When suggesting which to keep, prioritize: P1 commitments > external stakeholders > internal team > optional/recurring
