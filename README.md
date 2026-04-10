# AI PM — Personal PM Operating System

> *Not a chatbot. An operating system for product management.*

---

## What This Is

Most AI tools answer questions. This one runs your day.

**AI PM** is a personal operating system for senior product managers — a Claude-powered agent that reads your email, scans your calendar, monitors your Telegram and WhatsApp groups, processes meeting notes, and generates documentation. It aggregates signal from every channel you work in and returns structured, prioritized, project-aware output.

You don't ask it questions. You run commands. It does the work.

---

## The Mental Model

```
YOUR CHANNELS                  THE AGENT                   YOUR OUTPUT
─────────────────────────────────────────────────────────────────────────
  Gmail                ──┐
  Google Calendar      ──┤
  WhatsApp             ──┼──▶  skill routing  ──▶  project context  ──▶  briefing
  Telegram             ──┤     + live data         + priority ranking      PRDs
  Meeting Notes        ──┤     + schema contracts  + source citations      stories
  Confluence (soon)    ──┘                                                 follow-ups
```

Every piece of output is traced back to a source. No fabrication, no guessing, no hallucinated summaries.

---

## Commands

| Command | What it does |
|---|---|
| `/daily` | Morning briefing: email triage + calendar + messages + top 5 priorities |
| `/weekly` | Week planning: review + calendar analysis + project status + focus areas |
| `/triage` | Scan unread items across all channels, assign P1/P2/P3, associate with projects |
| `/followup` | Post-meeting: extract decisions + action items + draft follow-up messages |
| `/prd` | Generate a full PRD from project context using a structured template |
| `/analyze` | Analyze requirements against project scope — surfaces conflicts, risks, missing rules |
| `/spec` | Transform an approved PRD into a Functional Specification |
| `/issues` | Break an approved SPEC into sized, prioritized, sprint-ordered issues |
| `/devplan` | Generate a development plan + backend/QA story stubs for a single issue |
| `/qa` | Run QA test cycle, log bugs, track fixes, generate release checklist |

---

## The Product Lifecycle Workflow

This is the core workflow — the path from a stakeholder conversation to code in the development branch. Every step has a command, a gate, and a save location. Nothing is skipped.

```
/followup → /analyze → /prd → /spec → /issues → /devplan → /qa → checklist → push
```

Follow it in order. Each step's output is the next step's input.

---

### Step 1 — `/followup` — Extract Requirements from Meeting Notes

**What to do:** Run right after a stakeholder meeting. Paste your raw notes when asked.

**What you provide:** Raw meeting notes (paste or file path) + project name + meeting date

**What you get back:**
- Structured meeting notes with decisions, action items, and blockers
- Draft follow-up email and messages for your review
- A requirements draft ready for `/analyze`

**Gate:** Save the requirements file to `projects/<name>/docs/requirements/` before moving on.

---

### Step 2 — `/analyze` — Validate Requirements Against Scope

**What to do:** Run before writing the PRD. Feed it the requirements file from Step 1.

**What you provide:** Project name + path to requirements file

**What you get back:**
- Each requirement classified: New / Change / Conflict / Duplicate / Out of scope
- Business rule conflicts with source citations
- Missing rules and edge cases that are not yet governed
- Risk table with probability, impact, and mitigations
- A clear verdict: **Ready / Conditional / Not ready** to proceed to PRD

**Gate:** Resolve all conflicts and missing rules before moving to `/prd`. If Conditional, the agent tells you exactly what to fix first.

---

### Step 3 — `/prd` — Write the Product Requirements Document

**What to do:** Run after `/analyze` gives the green light.

**What you provide:** Project name + path to the requirements file

**What you get back:**
- A full PRD with problem statement, goals, user stories, scope, non-goals, risks, and timeline
- `[TBD]` markers for any missing information — nothing fabricated
- Draft presented for your review before saving

**Gate:** Change PRD status from `draft` to `approved` before running `/spec`. The agent enforces this.

---

### Step 4 — `/spec` — Generate the Functional Specification

**What to do:** Run after the PRD is approved.

**What you provide:** Project name + path to the approved PRD

**What you get back:**
- One FEAT section per PRD functional requirement, each with: user flow, business rules, acceptance criteria, and edge cases
- Data requirements, interface specs, and a complete error-state table
- All open questions flagged for your confirmation — nothing assumed

**Gate:** Approve the SPEC (change status to `approved`) before running `/issues`.

---

### Step 5 — `/issues` — Break the SPEC into Issues

**What to do:** Run after the SPEC is approved.

**What you provide:** Project name + path to approved SPEC + sprint capacity (optional)

**What you get back:**
- One issue file per SPEC feature, each with user story, acceptance criteria, DoD, size, and priority
- A summary table showing all issues, dependencies, and sprint order
- Sprint ordering recommendation with dependency rationale

**Gate:** Review and confirm the issue list. Issues blocked by unresolved SPEC TBDs are created but marked `blocked`.

---

### Step 6 — `/devplan` — Generate a Development Plan Per Issue

**What to do:** Run once per issue, in dependency order. This is the handoff to the developer.

**What you provide:** Project name + path to a single issue file

**What you get back (per issue):**
- **Dev plan** — technical approach, ordered implementation steps, affected files, business rules to enforce
- **Backend story stub** — endpoint specs, DB changes, acceptance criteria pre-filled from the issue
- **QA story stub** — test scenarios scaffolded from the acceptance criteria

**Gate:** Review all three documents before saving. The developer takes the dev plan + backend story; QA takes the QA story stub.

---

### Step 7 — `/qa` — Run the QA Test Cycle

**What to do:** Run after the developer marks the issue as implemented and deployed to the test environment.

**What you provide:** Project name + path to issue or dev plan

**What you get back:**
- Completed QA story with full test scenarios (happy path, edge cases, error states)
- Scenario-by-scenario walkthrough — you mark each as Pass or Fail
- Bug reports auto-generated on failure, with severity (P1/P2/P3), linked to the issue
- QA closure summary when all scenarios pass

**Gate:** All P1 bugs must be resolved and re-tested before moving to the release checklist.

---

### Step 8 — Release Checklist — Sign Off Before Pushing

**What to do:** Generated by `/qa` when the test cycle closes. Review and sign each item.

**What it covers:**
- [ ] All issues closed
- [ ] All QA stories passed
- [ ] No open P1 bugs
- [ ] All PRs reviewed and approved
- [ ] PRD and SPEC marked `approved`
- [ ] Stakeholder sign-off received

**Gate:** Every checkbox must be signed. The checklist is saved to `projects/<name>/docs/` as the permanent record.

---

### Step 9 — Push to Development Branch

**What to do:** PM authorizes. Developer pushes. Update issue statuses to `done` and update `projects/<name>/context.md` with the closed sprint.

---

### Why This Workflow

| Problem it solves | How |
|---|---|
| Requirements that contradict scope or existing rules | `/analyze` catches conflicts before a single line of the PRD is written |
| PRDs that developers can't implement | `/spec` expands intent into unambiguous acceptance criteria and edge cases |
| Developers guessing at implementation details | `/devplan` hands them a step-by-step technical roadmap |
| QA with no test plan | `/qa` generates scenario-based stories from the acceptance criteria you already wrote |
| Releases with no audit trail | Every step produces a saved, linked document — from requirements to release checklist |
| Knowledge locked in one person | The full document chain lives in `projects/` — any PM can pick up mid-cycle |
| Skipping steps under deadline pressure | Each command enforces its gate — a SPEC won't generate from a draft PRD |

Every feature that moves through this workflow produces a complete, traceable document trail: requirements → PRD → SPEC → issues → dev plans → stories → bug reports → release checklist. Nothing is lost between steps.

---

## Skills

The agent is composed of six independent skill modules. Each has its own scope, rules, MCP tooling, JSON schemas, prompts, and evaluation criteria.

```
skills/
├── email/         Gmail triage, prioritization, categorization, reply drafts
├── calendar/      Schedule reading, conflict detection, pre-meeting briefs
├── telegram/      Message reading, action extraction, context-aware replies
├── whatsapp/      Message reading, meeting scheduling from chat threads
├── meetings/      Note processing, action item extraction, task generation
└── docs/          PRDs, design docs, backend stories, QA stories
```

Skills communicate through a typed contract defined in `schemas/communication.json`. A message extracted from Telegram can trigger a calendar event or a task card without leaking format or context between layers.

---

## Multi-Project Architecture

Every operation is project-aware.

```
projects/
└── <project-name>/
    ├── context.md         goals, team, stakeholders, current sprint, channels
    ├── stakeholders.md    RACI matrix, communication preferences
    └── docs/
        ├── requirements/
        ├── prds/
        ├── specs/
        ├── issues/
        ├── design-docs/
        ├── meeting-notes/
        ├── stories/
        └── bugs/
```

When you run `/daily`, it aggregates signal across all active projects. When you run `/prd`, it pulls the right project's context, team, and sprint goals automatically. When a request is ambiguous, the agent asks — it never assumes.

---

## Templates

Every document generated by this system follows a structured template. Consistency is not a style preference — it is a rule.

| Template | Use Case |
|---|---|
| `requirements.md` | Raw requirements capture from stakeholder sessions |
| `prd.md` | Product Requirements Document — problem, goals, scope, requirements, timeline |
| `spec.md` | Functional Specification — features, business rules, acceptance criteria, edge cases |
| `issue.md` | Individual issue derived from SPEC — description, DoD, dependencies, size |
| `dev_plan.md` | Development plan per issue — approach, implementation steps, affected files |
| `design_doc.md` | Technical design — context, proposed solution, alternatives, rollout |
| `meeting_notes.md` | Decisions, actions, blockers, next steps |
| `backend_story.md` | Endpoint specs, DB changes, business rules, acceptance criteria |
| `qa_story.md` | Test scenarios in Given/When/Then format |
| `bug_report.md` | Bug report from QA — steps to reproduce, severity, fix approach |
| `release_checklist.md` | Definition of done before pushing to development branch |

---

## Schemas

Typed contracts for inter-skill communication and output validation.

```
schemas/
├── communication.json    universal message format between skills
├── task.json             action item format (owner, deadline, priority, source)
└── project_context.json  project file structure definition
```

Every task has an owner. Every message has a source. Every action item has a deadline. The schemas enforce this.

---

## Workflows

End-to-end processes that chain multiple skills together.

```
workflows/
├── daily_briefing.md          Email → Calendar → Messages → Top 5
├── weekly_planning.md         Review → Calendar → Projects → Focus Areas
├── meeting_lifecycle.md       Prep → Notes → Actions → Tasks → Follow-ups → Docs
├── documentation_flow.md      Any channel → Template → Review → Store → Link
├── requirements_analysis.md   Stakeholder session → Requirements → Scope analysis → PRD-ready
├── qa_testing.md              Implementation → QA story → Test cycle → Bug reports → Release
└── product_lifecycle.md       End-to-end PO workflow: steps 1–10 with commands and templates
```

---

## Rules

The agent has two governing documents that shape every response:

- **`rules/agent_rules.md`** — tool-first behavior, multi-project awareness, read/write safety, source citation, priority framework (P1/P2/P3)
- **`rules/communication_style.md`** — structured English, headers + bullets + tables over prose, mobile-first for messaging channels, formal for documentation

---

## Guardrails

| Rule | Why |
|---|---|
| Never send without explicit confirmation | Outbound messages are irreversible |
| Never delete emails, events, or messages | Archive only — no destructive actions |
| Never share content across channels without permission | Context belongs to the channel it came from |
| Never fabricate data | If a tool fails, say so. If data is missing, say so. |
| Always cite sources | Sender, subject, timestamp, event name, page URL |
| Always ask which project when ambiguous | Never guess context |
| Secrets stay in environment variables | Keys and tokens never appear in output, logs, or commits |

---

## MCP Integration Map

| Channel | MCP Server | Status |
|---|---|---|
| Gmail + Google Calendar | `taylorwilsdon/google_workspace_mcp` | Phase 1 |
| WhatsApp | `jlucaso1/whatsapp-mcp-ts` (Baileys) | Phase 2 |
| Telegram | `sparfenyuk/mcp-telegram` | Phase 2 |
| Confluence | `atlassian/atlassian-mcp-server` | Phase 6 |

The agent is built to degrade gracefully — commands work even when some MCP servers aren't connected yet. Available channels are processed; unavailable ones are noted in the output.

---

## Project Status

```
Phase 0 — Foundation        ████████████████████  complete
Phase 1 — Email + Calendar  ░░░░░░░░░░░░░░░░░░░░  next
Phase 2 — Messaging         ░░░░░░░░░░░░░░░░░░░░  planned
Phase 3 — Meetings          ░░░░░░░░░░░░░░░░░░░░  planned
Phase 4 — Docs + Stories    ░░░░░░░░░░░░░░░░░░░░  planned
Phase 5 — Evaluation        ░░░░░░░░░░░░░░░░░░░░  planned
Phase 6 — Confluence Sync   ░░░░░░░░░░░░░░░░░░░░  future
```

---

## Getting Started

1. Clone the repository
2. Copy `.env.example` to `.env` and configure your credentials
3. Open in Claude Code
4. Run `/daily`

No framework dependencies. No package.json. The logic lives in prompts, schemas, and rules — portable across any Claude-compatible environment.

---

## Design Principles

**Structured over conversational.** This is not a chat interface. Commands return tables, headers, and bullets — not paragraphs. Output is designed to be scanned, not read.

**Tool-first.** Every response is grounded in live data fetched via MCP. The agent does not reason from memory — it reads from sources.

**Write safety.** Reading is always automatic. Writing — sending a message, creating an event, generating a doc — always requires explicit confirmation.

**Modular.** Skills are independent. Schemas are contracts. You can swap, extend, or disable any skill without breaking the others.

**Project-aware by default.** The system does not operate in a vacuum. Every action belongs to a project. Every output is traceable to a source.

---

*Built with Claude Code. Designed for product leaders who operate across many simultaneous contexts and cannot afford noise.*
