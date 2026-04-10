# Weekly Planning Workflow

## Trigger
User runs `/weekly` command (suggested: Monday morning or Friday afternoon).

## Steps

### Step 1: Past Week Review
1. Review completed action items from the past week
2. Identify items that carried over (not completed)
3. Note key decisions made across all projects

### Step 2: Calendar Analysis
1. Fetch next week's calendar events
2. Identify heavy meeting days vs. light days
3. Flag events needing preparation
4. Detect conflicts or overload

### Step 3: Project Status
1. Read each active project's context file
2. Check current sprint status and goals
3. Identify any at-risk deliverables

### Step 4: Focus Areas
1. Generate **Top 5 Focus Areas** for the week
2. Map focus areas to specific days based on calendar availability
3. Suggest which meetings need prep and when to do it

## Output Format

```
# Weekly Planning — Week of [Date]

## Past Week Summary
- **Completed**: X action items across Y projects
- **Carried Over**: [List items that didn't get done]
- **Key Decisions**: [List major decisions made]

## This Week's Focus Areas
1. [Focus area] — [Project] — [Target deliverable]
2. ...

## Calendar Overview
| Day | Meetings | Free Hours | Heavy? |
|---|---|---|---|
| Mon | 3 (2h) | 6h | No |
| Tue | 6 (5h) | 3h | Yes |
| ... | | | |

## Key Meetings Requiring Prep
| Meeting | Day/Time | Prep Needed | Suggested Prep Time |
|---|---|---|---|
| | | | |

## Project Status
| Project | Sprint Status | At Risk? | Key Deliverable |
|---|---|---|---|
| | | | |

## Carried Over Items
| Item | Owner | Original Deadline | New Deadline |
|---|---|---|---|
| | | | |
```

## Dependencies
- Google Workspace MCP (calendar)
- Active project context files in `projects/`
- Previous meeting notes and action items
