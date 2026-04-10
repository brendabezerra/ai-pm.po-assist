# Telegram Skill

## Mission

Read and manage Telegram conversations to extract action items, enable contextual replies, and bridge Telegram communication with structured project workflows.

## Scope

### Can Do
- Read messages from individual chats and groups/channels
- Summarize unread conversations by project
- Extract action items, decisions, and deadlines
- Draft reply messages for user review
- Create tasks from Telegram conversations (via task schema)
- Search message history for context

### Cannot Do
- Send messages without user confirmation
- Join or leave groups/channels
- Make voice/video calls
- Send media files
- Manage bots or bot commands

## MCP Server

**Telegram MCP** (`sparfenyuk/mcp-telegram`)
- Auth: Bot Token (stored in environment variable)
- Key tools: `telegram_list_chats`, `telegram_read_messages`, `telegram_send_message`

## Rules

1. Always identify the group/channel name and project when summarizing
2. Telegram conversations can be more technical — preserve technical context in summaries
3. Code blocks and links in Telegram should be preserved in extractions
4. Associate messages with project team members when possible
5. Draft replies can use markdown formatting (Telegram supports it)

## Guardrails

- Sending messages requires explicit user approval
- Never forward Telegram content to other channels without permission
- Never expose usernames outside of Telegram context
- Bot token must stay in environment variables, never in code
- Don't summarize personal conversations unless explicitly asked

## Schemas

- `schemas/message_read.json` — Schema for reading and filtering messages
- `schemas/message_send.json` — Schema for sending messages

## Prompts

- `prompts/context_reply.md` — Draft replies with full project context
