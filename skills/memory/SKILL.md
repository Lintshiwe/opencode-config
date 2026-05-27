---
name: memory
description: Read and update a per-project memory file. Use at the start of every session to load project context, and whenever important decisions, architecture patterns, user preferences, or gotchas are established.
---

# Memory System

The memory file at `.opencode/memory.md` in the project root is your long-term memory. It persists across sessions.

## Startup (ALWAYS DO THIS FIRST)

When starting a session in any project:

1. Check if `.opencode/memory.md` exists in the project root
2. If it exists, read it fully. This contains the project's accumulated knowledge.
3. If it does NOT exist, create it with a basic skeleton after exploring the project.

## What to Store

Record these categories:

### Project Info
- Project name, purpose, tech stack (languages, frameworks, databases)
- Build commands, test commands, lint commands
- Entry points and key directories

### Architecture
- How the codebase is organized (monorepo structure, key modules)
- Data flow patterns, API design decisions
- Why certain architectural choices were made

### User Preferences
- Coding style preferences (tabs vs spaces, naming conventions)
- Technology preferences (preferred libraries, tools to avoid)
- How the user wants you to work (TDD? inline comments? etc.)

### Pitfalls & Gotchas
- Known issues, upgrade blockers, flaky tests
- Areas requiring special care
- Environment-specific quirks

### Decisions Log
- Key decisions made and WHY (format: YYYY-MM-DD - what & why)
- Rejected alternatives and the reasoning

## When to Update

- After ANY architectural decision is made
- When the user teaches you something about the project
- When you discover a gotcha or pitfall
- When dependencies or build commands change
- When new features fundamentally change the project

## Format

Keep it concise. Use sections. Update in-place -- don't grow endlessly. Remove outdated info. Target 50-200 lines.

```markdown
# Project: <name>

## Quick Start
- Build: <cmd>
- Test: <cmd>
- Lint: <cmd>

## Stack
- Frontend: <frameworks>
- Backend: <frameworks>
- Database: <db>
- Key dependencies: <list>

## Architecture
<key patterns and structure>

## User Preferences
<style and workflow preferences>

## Gotchas
<pitfalls and known issues>

## Decision Log
<dated decisions>
```

## NEVER

- Store secrets, tokens, passwords, or API keys
- Include sensitive PII (emails, names of real users, production data)
- Grow the file beyond ~300 lines -- summarize and compress
