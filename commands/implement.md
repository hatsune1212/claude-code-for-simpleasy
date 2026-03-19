---
description: Read a Linear ticket and implement the feature using TDD. Creates a feature branch, writes failing tests first, implements to pass them, commits, and produces handoff context for the E2E test agent.
---

# Implement Command

This command invokes the **feature-implementer** agent to implement a single Linear ticket using Test-Driven Development.

## What This Command Does

1. **Read SSOT Docs** - Load project-brief, scope-map, and domain-model
2. **Fetch Linear Ticket** - Read the ticket's full detail via MCP
3. **Plan Implementation** - List files and test files to create, wait for approval
4. **Create Feature Branch** - `feature/<TICKET-ID>` from main
5. **Write Tests First (RED)** - Failing tests from acceptance criteria
6. **Implement (GREEN)** - Minimum code to pass all tests
7. **Refactor (IMPROVE)** - Clean up with tests green
8. **Verify** - Run lint, format, type check, full test suite, coverage check
9. **Commit** - Structured commit message referencing the ticket
10. **Handoff** - Write `.handoff/last-feature.md` and post a Linear comment

## When to Use

Use `/implement <TICKET-ID>` when:
- A Linear ticket is ready for implementation
- After `/plan` has been approved for a ticket
- You want one focused PR for one ticket

## How It Works

The feature-implementer agent will:

1. **Read project docs** and the **Linear ticket**
2. **Output an implementation plan** (files, dependencies, out of scope)
3. **Wait for your approval** before writing any code
4. **Create a feature branch** (`feature/SIM-42`)
5. **Write the minimum code** that satisfies every acceptance criterion
6. **Run checks** (ruff, mypy, pytest) and fix any issues
7. **Commit** with a structured message linking back to the ticket
8. **Write handoff** in two places:
   - `.handoff/last-feature.md` — for the E2E test agent to read
   - Linear comment — visible on the ticket for the team
9. **Print a summary** confirming the branch, commit, and handoff

## Example Usage

```
User: /implement SIM-42

Agent (feature-implementer):
Reading docs and fetching ticket SIM-42...

## Implementation Plan

**Ticket:** SIM-42 — Invoice creation endpoint
**Branch:** feature/SIM-42

### Files to create
- src/models/invoice.py — Invoice SQLAlchemy model
- src/routes/invoices.py — POST /api/invoices endpoint
- src/schemas/invoice.py — Pydantic validation schema

### Files to modify
- src/routes/__init__.py — register invoice routes

### Dependencies
- None (SQLAlchemy and Pydantic already installed)

### Out of scope
- PDF export (separate ticket SIM-43)

Proceed? (yes/no/modify)
```

After approval:

```
Done — SIM-42: Invoice creation endpoint
Branch: feature/SIM-42
Commit: a1b2c3d feat(invoices): add invoice creation endpoint and model
Handoff: .handoff/last-feature.md + Linear comment posted
Ready for: E2E test agent
```

## Important Notes

- The agent will **NOT** write code until you approve the implementation plan
- It does **NOT** write tests — that is the E2E test agent's job
- One ticket = one branch = one commit = one PR
- If acceptance criteria are ambiguous, the agent leaves `# TODO: clarify` markers and flags them in the handoff
- Existing tests must still pass after implementation

## Integration with Other Commands

After implementation:
- Use `/e2e` to write and run E2E tests (reads `.handoff/last-feature.md`)
- Use `/code-review` to review the implementation
- Use `/build-fix` if the build breaks

Before implementation:
- Use `/plan <TICKET-ID>` to plan before implementing
- Use `/ticket` to generate tickets if none exist yet

## Related Agents

This command invokes the `feature-implementer` agent.

Source file: `agents/feature-implementer.md`
