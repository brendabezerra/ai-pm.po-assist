# Telegram Routing Eval

## Purpose
Test that the Telegram skill correctly processes messages, handles technical content, and routes to appropriate actions.

## Test Cases

### Case 1: Technical Content Preservation
**Input**: Message with code snippet and error log
**Expected**: Code blocks preserved in summary, technical context maintained

### Case 2: Action Item Extraction
**Input**: "Can someone review PR #234 and merge it before the release?"
**Expected**: Action item extracted — "Review and merge PR #234", context: before release

### Case 3: Channel vs Group Handling
**Input**: Message from a broadcast channel (read-only)
**Expected**: Categorized as fyi, no reply drafted

### Case 4: Link Extraction
**Input**: Message containing URLs to documentation or tickets
**Expected**: Links preserved and categorized in summary

### Case 5: Multi-Project Group
**Input**: Telegram group with messages about different projects
**Expected**: Messages correctly separated by project context

## Pass Criteria
- Technical content (code, links) preserved accurately
- Action items correctly extracted from informal messages
- Channel vs group distinction handled correctly
