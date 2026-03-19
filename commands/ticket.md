---
description: Generate implementation-ready feature tickets from project docs and create them in Linear. Breaks features into small, focused tickets sized for one PR each.
---

# Ticket Command

This command invokes the **ticket-writer** agent to generate and create Linear tickets grounded in the project's source-of-truth documents.

## What This Command Does

1. **Read SSOT Docs** - Load project-brief, scope-map, and domain-model
2. **Analyze Request** - Understand the feature to be broken down
3. **Propose Tickets** - Generate small, implementation-ready tickets
4. **Wait for Approval** - Present tickets for user validation
5. **Create in Linear** - Push approved tickets to the AI-PoC project

## When to Use

Use `/ticket` when:
- A new feature needs to be broken into implementation tasks
- You have a feature idea that needs structured tickets
- After `/plan` produces a plan that needs Linear tickets
- You want to populate the backlog for AI-driven development

## How It Works

The ticket-writer agent will:

1. **Read project docs** (project-brief.md, scope-map.md, domain-model.md)
2. **Analyze the feature request** and identify domain entities involved
3. **Generate one or more tickets**, each sized for one PR
4. **Present them for review** with full detail (acceptance criteria, technical notes, test suggestions)
5. **Wait for your approval** before creating anything in Linear
6. **Create issues in Linear** in the AI-PoC project

## Ticket Format

Each ticket includes:
- **Title** — concise feature description
- **Business Context** — why this matters
- **User Value** — what the user gains
- **Scope** — in scope / out of scope
- **Acceptance Criteria** — 3-7 precise bullets
- **Technical Notes** — affected entities, UI/backend areas, validation concerns
- **Suggested Tests** — happy path, error path, edge case
- **Open Questions** — anything unclear (never guessed)

## Example Usage

```
User: /ticket Add invoice creation with PDF export

Agent (ticket-writer):
I've read the project docs. Here are 3 tickets for this feature:

## Ticket 1: Invoice model and creation endpoint
Business Context: Core invoicing capability...
Acceptance Criteria:
- User can create an invoice via POST /api/invoices
- Invoice number is auto-generated (format: INV-YYYYMMDD-NNN)
- Required fields: client_name, line_items, due_date
- Validation rejects missing required fields
...

## Ticket 2: Invoice PDF generation
...

## Ticket 3: Invoice list and detail views
...

Create these 3 tickets in Linear? (yes/no/modify)
```

## Important Notes

- Tickets are created in the **AI-PoC** Linear project
- The agent will **NOT** create issues until you approve them
- All outputs are in **Japanese** (technical identifiers stay in English)
- The agent never invents business rules — unclear items go under Open Questions

## Integration with Other Commands

After ticket creation:
- Use `/plan <TICKET-ID>` to create a detailed implementation plan
- Use `/implement <TICKET-ID>` to implement the ticket
- Use `/e2e` after implementation to test the feature

## Related Agents

This command invokes the `ticket-writer` agent.

Source file: `agents/ticket-writer.md`
