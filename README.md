# OpenCode Global Config

<p align="center">
  <img src="https://img.shields.io/github/license/Lintshiwe/opencode-config?style=flat-square" alt="License: MIT">
  <img src="https://img.shields.io/github/stars/Lintshiwe/opencode-config?style=flat-square" alt="Stars">
  <img src="https://img.shields.io/github/issues/Lintshiwe/opencode-config?style=flat-square" alt="Issues">
  <img src="https://img.shields.io/badge/OpenCode-1.15.11-blue?style=flat-square" alt="OpenCode">
</p>

AI-powered coding with zero configuration overhead. This repo provides a complete [OpenCode](https://opencode.ai) setup with auto-routing backend/frontend agents, persistent per-project memory, parallel multi-agent development, automated code review, and desktop notifications -- all drop-in ready.

## Quick Start

```bash
git clone https://github.com/Lintshiwe/opencode-config.git
cp -r opencode-config/agents ~/.config/opencode/agents
cp -r opencode-config/skills ~/.config/opencode/skills
cp opencode-config/AGENTS.md ~/.config/opencode/AGENTS.md
cp opencode-config/opencode.jsonc ~/.config/opencode/opencode.jsonc
```

Restart OpenCode. Done.

---

## How It Works

### Auto-Routing (Zero Prompts)

You say what you need. The orchestrator detects the task type and silently dispatches to the right model. No buttons, no menus, no asking.

```
You:  "Create a REST API with JWT auth"
       |
       v          dispatch
Orchestrator ---------------> backend agent (deepseek-v4-pro)
                                    |
                                    v
                              Code generated, tests pass
                                    |
                                    v
                              notify-send "Task complete" ---> desktop popup
```

```
You:  "Build a login form with validation"
       |
       v          dispatch
Orchestrator ---------------> frontend agent (kimi-k2.6)
                                    |
                                    v
                              Components built, responsive, accessible
                                    |
                                    v
                              notify-send "Task complete" ---> desktop popup
```

### Parallel Full-Stack Development

When you need both backend and frontend, the orchestrator dispatches both agents simultaneously -- backend and frontend build in parallel, reducing wall-clock time. The orchestrator shares findings between them to eliminate duplicate work.

```
You:  "Build a todo app with React frontend and Express API"

       Orchestrator
        ↙         ↘
   backend        frontend
   (deepseek)     (kimi-k2.6)
       |              |
   POST /todos    <TodoList />
   GET /todos     <AddTodo />
       |              |
       `---- integrate --'
              |
         Shared API types
         No duplicate exploration
              |
      notify-send "App ready"
```

### Per-Project Memory

Every project gets a `.opencode/memory.md` file that the agent reads on startup and updates as you work. Stores architecture decisions, build commands, user preferences, and gotchas -- so you never repeat yourself.

```
Session 1:
  > "We use pnpm, not npm"
  > "Tests run with vitest, not jest"
  > SAVED to .opencode/memory.md

Session 2 (weeks later):
  > Agent reads memory.md automatically
  > Knows: pnpm, vitest, project structure
  > No re-explanation needed
```

### Automated Code Review (`simplify`)

Run `simplify` and three review agents launch in parallel:
1. **Code Reuse** -- finds duplicate logic, suggests existing utilities
2. **Code Quality** -- flags redundant state, parameter sprawl, anti-patterns
3. **Efficiency** -- detects missed concurrency, N+1 queries, memory leaks

### Desktop Notifications

When any task completes, `notify-send` fires a desktop popup so you don't have to watch the terminal.

---

## What's Inside

### Agents

| Agent | Model | Used For |
|---|---|---|
| `backend` | deepseek-v4-pro | APIs, databases, auth, CLI, DevOps, infrastructure |
| `frontend` | kimi-k2.6 | UI components, styling, layouts, animations, UX |
| `explore` | default | File search, codebase exploration, research |

All agents are `mode: all` -- switch via `/agent backend` or `/agent frontend`.

### Skills

| Skill | Description |
|---|---|
| `simplify` | Three-phase code review (reuse, quality, efficiency) |
| `memory` | Auto-loading/updating per-project memory file |

### Plugins

| Plugin | What It Does |
|---|---|
| `superpowers` | TDD, brainstorming, debugging, code review, git worktrees |
| `oh-my-opencode-slim` | Lightweight agent orchestration layer |
| `opencode-magi` | Multi-agent PR review and merge automation |
| `opencode-subagent-statusline` | Live subagent session status in TUI |
| `@tarquinen/opencode-dcp` | Context pruning to reduce token costs |
| `@distlang/opencode-plugin` | Session capture to Distlang Agent Debugger |

---

## File Structure

```
opencode-config/
├── README.md
├── LICENSE                     # MIT
├── AGENTS.md                   # Auto-routing, memory, parallel agents, notifications
├── opencode.jsonc              # Plugin registry
├── agents/
│   ├── backend.md              # deepseek-v4-pro
│   └── frontend.md             # kimi-k2.6
├── skills/
│   ├── simplify/SKILL.md       # Code review automation
│   └── memory/SKILL.md         # Per-project persistent memory
└── sessions/
    └── *.json                  # Exported session transcripts
```

---

## Security

- `.opencode/memory.md` is globally gitignored -- never committed
- Zero secrets, tokens, or credentials in any file
- Memory files are local-only, per-project scope
- Config is installation instructions, not runtime code

---

## Requirements

- [OpenCode](https://opencode.ai) >= 1.15
- `notify-send` (libnotify) for desktop notifications
- Git for version-control integration

---

## Share

Help others discover this config:

[![Tweet](https://img.shields.io/badge/Share_on-Twitter/X-1DA1F2?style=for-the-badge&logo=x&logoColor=white)](https://twitter.com/intent/tweet?text=Auto-routed%20AI%20coding%20agents%20for%20OpenCode%20%E2%80%94%20backend%20%2B%20frontend%20in%20parallel,%20per-project%20memory,%20code%20review,%20desktop%20notifications&url=https://github.com/Lintshiwe/opencode-config&hashtags=OpenCode,AI,DeveloperTools)
[![Reddit](https://img.shields.io/badge/Post_on-Reddit-FF4500?style=for-the-badge&logo=reddit&logoColor=white)](https://www.reddit.com/r/opencode/submit?url=https://github.com/Lintshiwe/opencode-config&title=OpenCode%20Global%20Config%20-%20Auto-routed%20backend/frontend%20agents%20with%20memory)
[![Dev.to](https://img.shields.io/badge/Blog_on-Dev.to-0A0A0A?style=for-the-badge&logo=devdotto&logoColor=white)](https://dev.to/new?url=https://github.com/Lintshiwe/opencode-config)
[![LinkedIn](https://img.shields.io/badge/Post_on-LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/sharing/share-offsite/?url=https://github.com/Lintshiwe/opencode-config)
[![Hacker News](https://img.shields.io/badge/Post_on-Hacker_News-FF6600?style=for-the-badge&logo=ycombinator&logoColor=white)](https://news.ycombinator.com/submit?url=https://github.com/Lintshiwe/opencode-config&title=OpenCode%20Global%20Config)

### Copy-Paste Post Templates

**Twitter/X:**
```
I set up @opencode_ai with auto-routing so backend tasks use deepseek-v4-pro and frontend uses kimi-k2.6 — completely automatic, no prompts.

+ Per-project memory across sessions
+ Parallel backend + frontend agents
+ Automated code review (simplify)
+ Desktop notifications on completion

All configs, zero code: https://github.com/Lintshiwe/opencode-config
```

**Reddit (r/opencode, r/programming):**
```
Title: I built an OpenCode config that auto-routes work to the best AI model

OpenCode lets you define custom agents with different models. I set up:

- backend agent → deepseek-v4-pro (APIs, databases, auth)
- frontend agent → kimi-k2.6 (UI, components, styling)
- Auto-detection of task type — no manual switching
- Parallel agents for full-stack work (backend + frontend at once)
- Per-project memory file that persists across sessions
- Automated code review with 3 parallel subagents
- Desktop notifications when work completes

Everything is in one repo — drop the files into ~/.config/opencode and restart.

https://github.com/Lintshiwe/opencode-config
```

**LinkedIn:**
```
As AI coding tools evolve, the key differentiator isn't the model — it's the orchestration.

I configured OpenCode to automatically route different types of work to different AI models:
• Backend → deepseek-v4-pro
• Frontend → kimi-k2.6
• Research → default explorer

The orchestrator detects task type silently, dispatches work, and even runs backend + frontend agents in parallel for full-stack projects.

Bonus features: per-project long-term memory, automated code review, subagent status tracking, context pruning for token efficiency.

Open source, MIT licensed. All configs, no code: https://github.com/Lintshiwe/opencode-config
```

**Discord / Slack (short):**
```
OpenCode auto-routing config — backend (deepseek-v4-pro) + frontend (kimi-k2.6) with per-project memory, parallel agents, code review, and notifications. Drop-in ready: https://github.com/Lintshiwe/opencode-config
```

---

## Contributing

Issues, PRs, and discussions welcome. This is a public utility repo -- if you have improvements to agent configurations, skills, or workflows, open a PR.

---

## License

MIT -- see [LICENSE](LICENSE)
