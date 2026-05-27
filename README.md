# OpenCode Global Configuration

Custom agents, skills, and plugins for OpenCode AI coding assistant. Auto-routes backend/frontend work to specialized models, persists per-project memory, and enables multi-agent workflows.

## Installation

Clone and symlink:

```bash
git clone <this-repo> ~/opencode-config
cp -r ~/opencode-config/agents ~/.config/opencode/agents
cp -r ~/opencode-config/skills ~/.config/opencode/skills
cp ~/opencode-config/AGENTS.md ~/.config/opencode/AGENTS.md
cp ~/opencode-config/opencode.jsonc ~/.config/opencode/opencode.jsonc
```

Restart OpenCode after install.

---

## Agents

### `backend` — deepseek-v4-pro
Auto-dispatched for all server-side work: APIs, databases, auth, CLI tools, DevOps, infrastructure.

### `frontend` — kimi-k2.6
Auto-dispatched for all client-side work: UI components, styling, layouts, animations, UX.

Both agents are `mode: all` — usable as primary (`/agent backend`) or as subagents dispatched by the orchestrator.

---

## Skills

### `simplify` — Code Review & Cleanup
Three-phase automated code review (reuse, quality, efficiency) launched as parallel subagents. Reviews git changes, finds duplicate code, flags anti-patterns, and fixes issues.

**Source:** [AbdoKnbGit/opencode-simplify](https://github.com/AbdoKnbGit/opencode-simplify)

### `memory` — Per-Project Memory
Auto-loads `.opencode/memory.md` from the project root every session. Auto-updates it when decisions are made, preferences are stated, or pitfalls are discovered. Never committed to git (`.opencode/` is globally gitignored).

---

## Auto-Routing

The orchestrator agent NEVER writes code itself. It detects task type and silently dispatches:

| Task Type | Model |
|---|---|
| Backend (APIs, DB, auth, CLI, DevOps) | deepseek-v4-pro |
| Frontend (UI, styling, components, UX) | kimi-k2.6 |
| Research / exploration | default |

No user prompts, no confirmation — fully automatic.

---

## Plugins Installed (via opencode.jsonc)

| Plugin | Purpose |
|---|---|
| `superpowers` | Development workflows (TDD, brainstorming, debugging, code review, git worktrees) |
| `oh-my-opencode-slim` | Lightweight agent orchestration |
| `opencode-magi` | Multi-agent PR review and merge |
| `opencode-subagent-statusline` | Shows subagent session status in TUI |
| `@tarquinen/opencode-dcp` | Prunes stale context to reduce token costs |
| `@distlang/opencode-plugin` | Session capture to Distlang Agent Debugger |

---

## Security

- `.opencode/memory.md` is globally gitignored — never pushed
- No secrets, tokens, or API keys in any file
- Memory files are local-only, project-scoped

---

## File Map

```
opencode-config/
├── README.md           # This file
├── AGENTS.md           # Global agent instructions (auto-routing, memory, rules)
├── opencode.jsonc       # Global opencode config (plugins)
├── agents/
│   ├── backend.md       # deepseek-v4-pro backend agent
│   └── frontend.md      # kimi-k2.6 frontend agent
└── skills/
    ├── simplify/SKILL.md    # Automated code review skill
    └── memory/SKILL.md      # Per-project persistent memory skill
```
