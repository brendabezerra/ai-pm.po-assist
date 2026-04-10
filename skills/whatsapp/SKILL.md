# WhatsApp Skill

## Mission

Read and manage WhatsApp conversations to extract action items, schedule meetings from chat context, and enable contextual replies. Bridge informal communication with structured project management.

## Scope

### Can Do
- Read messages from individual chats and groups
- Summarize unread conversations by project
- Extract action items, decisions, and deadlines from messages
- Draft reply messages for user review
- Schedule meetings from chat discussions (via communication schema → calendar)
- Create tasks from WhatsApp conversations (via task schema)

### Cannot Do
- Send messages without user confirmation
- Join or leave groups
- Make voice/video calls
- Send media files
- Access messages from before the MCP session was established

## MCP Server

**WhatsApp MCP** (`jlucaso1/whatsapp-mcp-ts`)
- Auth: QR code pairing via Baileys
- Session stored locally (never committed)
- Key tools: `whatsapp_list_chats`, `whatsapp_read_messages`, `whatsapp_send_message`

## Rules

1. Always identify the group/chat name and project when summarizing
2. Extract names and associate with known team members from project context
3. Messages are informal — interpret intent, don't quote literally unless asked
4. When creating tasks from WhatsApp, cite the message sender and approximate timestamp
5. Respect the informal nature — draft replies should match WhatsApp tone (see communication_style.md)

## Guardrails

- Sending messages requires explicit user approval
- Never forward WhatsApp content to email or other channels without permission
- Never expose phone numbers outside of WhatsApp context
- Don't summarize personal/non-work conversations unless explicitly asked
- Session tokens must stay in local storage, never in code or config

## Schemas

- `schemas/message_read.json` — Schema for reading and filtering messages
- `schemas/message_send.json` — Schema for sending messages

## Prompts

- `prompts/meeting_schedule.md` — Extract meeting request from chat and create calendar event
