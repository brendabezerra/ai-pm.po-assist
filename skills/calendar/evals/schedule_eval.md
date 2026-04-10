# Schedule Eval

## Purpose
Test that the calendar skill correctly reads schedules, detects conflicts, and formats daily briefings.

## Test Cases

### Case 1: Conflict Detection
**Input**: Two events at 10:00-11:00 on the same day
**Expected**: Hard conflict flagged with suggestion on which to keep

### Case 2: Buffer Conflict
**Input**: Event A ends at 11:00, Event B starts at 11:00
**Expected**: Buffer conflict flagged, suggest 10-minute gap

### Case 3: Overload Detection
**Input**: 6 hours of meetings in one day
**Expected**: Overload warning flagged

### Case 4: Prep Needed Detection
**Input**: Meeting titled "Board Presentation" with 5 external attendees
**Expected**: Marked as needs_prep = true

### Case 5: Free Block Identification
**Input**: Meetings at 9-10, 11-12, 14-15 on a standard 9-18 workday
**Expected**: Free blocks identified: 10-11, 12-14, 15-18

### Case 6: Project Association
**Input**: Meeting with attendees who are known members of Project Y
**Expected**: Event associated with Project Y

## Pass Criteria
- All hard conflicts detected (zero false negatives)
- Free blocks correctly calculated
- Prep detection for external/stakeholder meetings > 90%
