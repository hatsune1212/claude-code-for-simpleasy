---
description: Build the initial webapp scaffold from project docs. Creates folder structure, domain types, routing shell, and dev tooling without implementing features.
---

# Scaffold Command

This command invokes the **skeleton-builder** agent to create or refine the initial application scaffold.

## What This Command Does

1. **Read SSOT Docs** - Load project-brief, scope-map, and domain-model
2. **Inspect Repo** - Identify what already exists vs what is missing
3. **Propose Scaffold** - List folders and files to create, wait for approval
4. **Build Structure** - Create the minimum scaffold required
5. **Configure Tooling** - Set up lint, format, and test runner
6. **Verify** - Run basic checks to ensure the scaffold is valid

## When to Use

Use `/scaffold` when:
- Starting a new project from scratch
- Setting up folder structure for a new module
- Wiring up a design system or CSS framework
- Preparing a repo for ticket-driven development
- Adding dev tooling (linter, formatter, test runner)

## How It Works

The skeleton-builder agent will:

1. **Read project docs** (project-brief.md, scope-map.md, domain-model.md)
2. **Scan the repo** to see what already exists
3. **Propose a scaffold plan** with exact folders and files
4. **Wait for your approval** before creating anything
5. **Build the scaffold** with explicit TODO placeholders
6. **Verify** that imports, lint, and test runner work
7. **Summarize** what is ready for ticket-driven development

## Example Usage

```
User: /scaffold

Agent (skeleton-builder):
## Scaffold Plan

### Folders to create
- src/models/ — domain entities from domain-model.md
- src/routes/ — route registry with placeholders
- src/services/ — business logic stubs
- src/templates/ — base layout shell
- tests/ — test configuration

### Files to create
- src/models/invoice.py — Invoice entity
- src/models/user.py — User entity
- src/routes/__init__.py — route registry
- pyproject.toml — project config with dependencies
- .ruff.toml — linter config

### Out of scope
- Invoice creation logic (ticket-driven)
- Authentication flow (ticket-driven)

Proceed with this scaffold? (yes/no/modify)
```

## Important Notes

- The agent will **NOT** create any files until you approve the plan
- All generated code uses explicit `# TODO:` placeholders — no business logic is guessed
- Domain entity names come directly from `docs/domain-model.md`

## Integration with Other Commands

After scaffolding:
- Use `/ticket` to generate implementation tickets from the scaffold
- Use `/plan` to plan a specific feature
- Use `/implement` to implement a ticket

## Related Agents

This command invokes the `skeleton-builder` agent.

Source file: `agents/skeleton-builder.md`
