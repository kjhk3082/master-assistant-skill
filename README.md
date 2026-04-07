# Master Assistant for Claude Code

<div align="center">

[![Claude Code Skill](https://img.shields.io/badge/Claude_Code-Skill-7B61FF?style=for-the-badge&logo=anthropic&logoColor=white)](https://github.com/kjhk3082/master-assistant-skill)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](CONTRIBUTING.md)
[![GitHub Stars](https://img.shields.io/github/stars/kjhk3082/master-assistant-skill?style=for-the-badge)](https://github.com/kjhk3082/master-assistant-skill/stargazers)

**The definitive skill for unlocking 100% of Claude Code's capabilities.**

[한국어](#한국어) · [English](#english) · [Installation](#-installation) · [Usage](#-usage)

</div>

---

## English

**Master Assistant** is a Claude Code skill that forces the agent to utilize **every single built-in capability** — Plan Mode, Subagents, Agent Teams, Hooks, MCP, Channels, Scheduled Tasks, Remote Control, 40 built-in tools, 60+ slash commands, Permission Enforcement, LSP, Task Registry, and more — without missing a single feature.

### Why This Skill Exists

> *The bottleneck is no longer typing speed. When agent systems can rebuild a codebase in hours, the scarce resource becomes architectural clarity, task decomposition, judgment, and conviction about what is worth building.*

Most Claude Code users tap into less than 30% of its actual capabilities. This skill closes that gap by encoding a complete operating manual directly into the agent's context.

### What's Inside

| Feature | Description |
|---------|-------------|
| **Pre-flight Checklist** | `/doctor`-level environment validation before every task |
| **Scenario Routing Table** | Automatic selection of the right mode for each task type |
| **Three-Layer Engineering** | Prompt → Context → Harness design principles |
| **40 Built-in Tools Guide** | Complete reference for all tools with permission levels |
| **60+ Slash Commands** | Categorized reference for every slash command |
| **4-Phase Workflow** | Plan → Execute → Verify → Handoff with templates |
| **Hooks Lifecycle** | PreToolUse / PostToolUse / Stop / Notification automation |
| **Auto-Harness & Knowledge Base** | Self-learning system that accumulates patterns and gotchas |
| **UI/UX Design System** | Professional-grade design rules enforced during code generation |
| **Security Assessment** | OWASP Top 10 based vulnerability checks |
| **Anti-Pattern Prevention** | 7 common failure patterns with solutions |
| **Model Aliases & Config Precedence** | Complete reference for settings and model selection |

---

## 한국어

**Master Assistant**는 Claude Code 에이전트가 자신의 **모든 기능을 100% 활용**하도록 강제하는 완전 운영 매뉴얼 스킬입니다.

Plan Mode, Subagents, Agent Teams, Hooks, MCP, Channels, Scheduled Tasks, Remote Control, **40개 내장 도구**, **60개 이상의 슬래시 커맨드**, Permission Enforcement, LSP, Task Registry 등 단 하나의 기능도 빠짐없이 활용합니다.

### 이 스킬이 필요한 이유

대부분의 Claude Code 사용자는 실제 기능의 30% 미만만 활용합니다. 이 스킬은 완전한 운영 매뉴얼을 에이전트의 컨텍스트에 직접 인코딩하여 그 격차를 해소합니다.

---

## 📦 Installation

### Option 1: Claude Code Skill Manager (Recommended)

```bash
/skills install https://github.com/kjhk3082/master-assistant-skill
```

### Option 2: Manual Installation

```bash
# Clone the repository
git clone https://github.com/kjhk3082/master-assistant-skill.git

# Copy SKILL.md to your project's skill directory
mkdir -p your-project/.claude/skills/master-assistant
cp master-assistant-skill/SKILL.md your-project/.claude/skills/master-assistant/
```

### Option 3: Global Installation

```bash
# Install globally for all projects
mkdir -p ~/.claude/skills/master-assistant
cp SKILL.md ~/.claude/skills/master-assistant/
```

---

## 🚀 Usage

Once installed, invoke the skill explicitly or let Claude Code reference it automatically.

### Explicit Invocation

```
@master-assistant Follow the pre-flight checklist and plan a refactoring for this project.
```

### Built-in Slash Commands

```bash
# UI/UX Design System
/ui-component LoginForm        # Generate a component following design system rules
/ui-review src/components/     # Audit existing code for design violations
/ux-audit src/pages/Home.tsx   # Nielsen heuristics-based UX audit

# Security Assessment
/security-review src/auth/     # OWASP Top 10 vulnerability analysis
/sec-fix src/api/users.ts      # Auto-refactor security vulnerabilities

# Deep Planning
/ultraplan "Migrate monolith to microservices"  # Multi-step reasoning plan
```

### Workflow Example

```
1. Start a new task:
   "Refactor the authentication module"

2. Claude Code will automatically:
   ✓ Run pre-flight checks (read CLAUDE.md, check git status)
   ✓ Enter Plan Mode and create plan.md
   ✓ Assess blast radius before any changes
   ✓ Execute with appropriate permission mode
   ✓ Run verification (lint, tests, /review)
   ✓ Write handoff.md on session end
   ✓ Update docs/wiki/patterns.md with learnings
```

---

## 📁 Recommended Project Structure

This skill recommends maintaining the following structure in your project:

```text
repo/
├── CLAUDE.md                    # Core operating rules (≤80 lines, always loaded)
├── CLAUDE.local.md              # Local-only rules (add to .gitignore)
├── .claude/
│   ├── settings.json            # Permission boundaries, Hooks, MCP servers
│   ├── settings.local.json      # Local overrides (add to .gitignore)
│   └── rules/                   # Path-specific rules
├── docs/
│   ├── wiki/
│   │   ├── patterns.md          # Auto-accumulated coding patterns
│   │   ├── gotchas.md           # Lessons learned, pitfalls
│   │   └── retrospective.md     # Per-session retrospectives
│   └── dashboard.md             # Project status dashboard
├── plan.md                      # Current task plan (written before execution)
└── handoff.md                   # Handoff notes (updated on session end)
```

---

## ⚙️ Hooks Configuration Example

Add this to `.claude/settings.json` to enable automatic knowledge accumulation:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "write_file|edit_file",
        "hooks": [{"type": "command", "command": "npm run lint --fix 2>/dev/null || true"}]
      }
    ],
    "Stop": [
      {
        "hooks": [{"type": "command", "command": "node scripts/update-handoff.js 2>/dev/null || true"}]
      }
    ],
    "Notification": [
      {
        "hooks": [{"type": "command", "command": "osascript -e 'display notification \"Claude Code: Task complete\"' 2>/dev/null || true"}]
      }
    ]
  }
}
```

---

## 🔑 Key Principles

### The Three-Layer Engineering Model

```
Layer 1: Prompt Engineering
  └─ Short, structured instructions with XML tags
  └─ Clear Done When criteria

Layer 2: Context Engineering
  └─ @file references, !command injection
  └─ /compact, /clear, /context management

Layer 3: Harness Engineering
  └─ Permission boundaries (read-only → workspace-write → danger-full-access)
  └─ Hooks for automated verification
  └─ Verification loops before automation
```

### The Blast Radius Principle

> Local, reversible actions (editing files, running tests) are usually fine.  
> Actions that affect shared systems, publish state, delete data, or have high blast radius  
> **must be explicitly authorized** by the user or durable workspace instructions.

### The Automation Ladder

```
Step 1: Rules        → Write clear CLAUDE.md instructions
Step 2: Verification → Build tests, lint, CI
Step 3: State        → Maintain plan.md, handoff.md, wiki
Step 4: Skills       → Skillify repetitive tasks
Step 5: MCP          → Connect external services
Step 6: Automation   → Add Hooks, Cron, Channels
```

---

## 📊 What's Covered

<details>
<summary><strong>40 Built-in Tools (Click to expand)</strong></summary>

| Category | Tools |
|----------|-------|
| File Operations | `read_file`, `write_file`, `edit_file`, `glob_search`, `grep_search` |
| Execution | `bash`, `REPL`, `NotebookEdit`, `Sleep` |
| Web | `WebFetch`, `WebSearch` |
| Agents | `Agent`, `Skill`, `ToolSearch`, `TodoWrite` |
| Planning | `EnterPlanMode`, `ExitPlanMode`, `StructuredOutput`, `AskUserQuestion` |
| Config | `Config`, `SendUserMessage`, `RemoteTrigger` |
| Task Registry | `TaskCreate`, `TaskGet`, `TaskList`, `TaskStop`, `TaskUpdate`, `TaskOutput` |
| Team/Cron | `TeamCreate`, `TeamDelete`, `CronCreate`, `CronDelete`, `CronList` |
| MCP | `ListMcpResources`, `ReadMcpResource`, `McpAuth`, `MCP` |
| LSP | `LSP` (diagnostics, hover, definition, references, symbols) |

</details>

<details>
<summary><strong>60+ Slash Commands (Click to expand)</strong></summary>

| Category | Commands |
|----------|----------|
| Session | `/status`, `/cost`, `/usage`, `/compact`, `/clear`, `/context`, `/files`, `/memory` |
| Planning | `/plan`, `/ultraplan`, `/tasks`, `/diff`, `/branch`, `/commit`, `/pr`, `/issue` |
| Quality | `/review`, `/bughunter`, `/security-review`, `/release-notes` |
| Skills | `/skills`, `/plugin`, `/agents`, `/mcp` |
| Diagnostics | `/doctor`, `/config`, `/hooks`, `/permissions`, `/model`, `/sandbox` |
| Advanced | `/thinkback`, `/insights`, `/advisor`, `/brief`, `/effort`, `/teleport`, `/debug-tool-call` |
| Session Ops | `/undo`, `/stop`, `/retry`, `/rewind`, `/session`, `/resume`, `/export` |

</details>

---

## 🤝 Contributing

Contributions are welcome! Bug reports, feature suggestions, and pull requests are all appreciated.

1. Fork this repository
2. Create a new branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

---

## 📄 License

This project is distributed under the MIT License. See [LICENSE](LICENSE) for more information.

---

<div align="center">

**If this skill saves you time, please consider giving it a ⭐**

[Report Bug](https://github.com/kjhk3082/master-assistant-skill/issues) · [Request Feature](https://github.com/kjhk3082/master-assistant-skill/issues) · [Discussions](https://github.com/kjhk3082/master-assistant-skill/discussions)

</div>
