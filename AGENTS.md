# Agent Instructions

## Memory — Persist Across Sessions

At the START of every session in any project, read `.opencode/memory.md` in the project root. This is the project's long-term memory -- architecture decisions, user preferences, gotchas, and build commands accumulated across sessions.

When important facts are established (decisions made, preferences stated, pitfalls discovered), IMMEDIATELY update `.opencode/memory.md`. Never ask permission to write to memory. Just do it.

NEVER commit `.opencode/memory.md` to git. It is local-only. `.opencode/` is globally gitignored.

## Auto-Routing (DO NOT ASK USER FOR CONFIRMATION)

For ANY implementation task, silently auto-dispatch to the correct agent. NEVER implement directly. NEVER ask permission. Just dispatch:

| Task type | Dispatch to | Model |
|---|---|---|
| Backend (APIs, databases, auth, server logic, CLI, DevOps, infrastructure) | `backend` agent | deepseek-v4-pro |
| Frontend (UI components, styling, layouts, client logic, animations, UX) | `frontend` agent | kimi-k2.6 |
| Exploration, research, file search | `explore` agent | (default) |

Your ONLY job is orchestration, planning, and review. You write ZERO implementation code yourself.

## Permanent Rules

### Icons — NEVER use emojis
For all UI work, ALWAYS use professional SVG icon libraries. Emojis are never acceptable.

**Approved icon sources (in preference order):**
1. `lucide-react` — `npm install lucide-react`
2. `@heroicons/react` — `npm install @heroicons/react`
3. `@phosphor-icons/react` — `npm install @phosphor-icons/react`
4. `@iconify/react` — `npm install @iconify/react @iconify/icons-heroicons`

**Icon naming conventions by library:**
| Concept | lucide | Heroicons | Phosphor |
|---|---|---|---|
| Dashboard | `ChartBar` | `ChartBarIcon` | `ChartBar` |
| Users | `Users` | `UsersIcon` | `Users` |
| Projects | `FolderKanban` | `FolderIcon` | `Folders` |
| Settings | `Settings` | `Cog6ToothIcon` | `GearSix` |
| Edit | `Pencil` | `PencilIcon` | `PencilSimple` |

**If you need an icon and can't find it in the installed library:**
1. Search https://phosphoricons.com
2. Search https://heroicons.com
3. Search https://icon-sets.iconify.design
4. Search https://www.flaticon.com
5. Install the appropriate library, then use the icon

**Full icon resource guide**: See `~/.config/opencode/icons.md` for complete reference including Tabler, FontAwesome, Bootstrap Icons, Iconify, LottieFiles, Icons8, and Flaticon.

## DESIGN.md — UI/UX Consistency

Always read and follow `./DESIGN.md` before making any UI, styling, layout, or component changes. If `./DESIGN.md` doesn't exist in the current project, fall back to `~/.config/opencode/DESIGN.md` (the global default — Voltagent Inspired).

If no DESIGN.md exists anywhere, install one with:

`npx designmd.sh add <owner/repo> -y --no-telemetry`

For DESIGN.md management, use these commands:

- `npx designmd.sh list`
- `npx designmd.sh update`
- `npx designmd.sh add <owner/repo>`
- `npx designmd.sh remove [name]`
- `npx designmd.sh init [name]`

## Superpowers — Development Workflows

These workflows are MANDATORY. Follow them in every project.

### 1. Brainstorming (before any creative work)
- Before creating features, building components, adding functionality, or modifying behavior, explore user intent, requirements, and design first
- Propose 2-3 approaches with trade-offs before implementation
- Write a design doc to `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`
- Get user approval on the written spec before touching code
- **HARD GATE: NO implementation before design approval**

### 2. Test-Driven Development
- **IRON LAW: NO production code without a failing test first**
- RED: Write one minimal failing test → verify it fails for the right reason
- GREEN: Write simplest code to pass → verify it passes
- REFACTOR: Clean up (remove duplication, improve names) → keep tests green
- Never skip TDD because "it's too simple". Simple code breaks. Tests take seconds.

### 3. Systematic Debugging
- **IRON LAW: NO fixes without root cause investigation first**
- Phase 1: Root cause investigation (read errors, reproduce, trace data flow)
- Phase 2: Pattern analysis (find working examples, compare, identify differences)
- Phase 3: Form single hypothesis, test minimally (one variable at a time)
- Phase 4: Create failing test → implement single fix → verify
- If 3+ fixes fail: question the architecture, not the hypothesis
- Use defense-in-depth: validate at EVERY layer data passes through

### 4. Verification Before Completion
- **IRON LAW: NO completion claims without fresh verification evidence**
- Identify what command proves the claim → run it FRESH → read full output → verify
- Skip any step = lying, not verifying
- Never claim "tests pass" from memory. Always re-run.

### 5. Code Review
- Request code review after completing tasks, before merging
- When receiving review: READ → UNDERSTAND → VERIFY → EVALUATE → RESPOND → IMPLEMENT
- Never performative agreement ("You're right!", "Great point!"). Just fix it.
- Fix priority: blocking issues → simple fixes → complex fixes

### 6. Writing Plans (before multi-step implementation)
- Write comprehensive plans assuming zero context
- Document: files to touch, code, testing, docs
- Bite-sized tasks (2-5 min each): test → code → verify → commit
- Save to `docs/superpowers/plans/YYYY-MM-DD-<feature-name>.md`
- No placeholders (TBD, TODO, "implement later" are plan failures)

### 7. Subagent-Driven Development (for complex plans)
- Execute plans by dispatching fresh subagent per task
- Two-stage review per task: spec compliance first, then code quality
- Never dispatch multiple implementation subagents in parallel
- Use git worktrees for feature isolation

### 8. Git Worktrees
- Create isolated workspace for each feature branch
- Detect existing isolation before creating new
- Verify clean baseline (run tests) before starting

## Priority
1. User's explicit instructions — highest
2. These instructions (AGENTS.md + DESIGN.md)
3. Superpowers skills
4. Default system prompt — lowest
