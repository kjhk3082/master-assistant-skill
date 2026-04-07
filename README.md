# Master Assistant Skill for Claude Code

![Hero Banner](assets/hero-banner.png)

A complete, battle-tested skills framework for Claude Code that enforces a strict, professional software development workflow. 

Unlike simple prompt templates, this is a **collection of interconnected skills** that automatically trigger based on context, forcing Claude Code to plan, verify, and document its work properly.

## 🌟 Why Use This?

Out of the box, Claude Code is powerful but can be chaotic. It might overwrite files without asking, skip tests, or lose context between sessions. 

This skill collection fixes that by enforcing a **4-Stage Workflow**:

![Workflow Diagram](assets/workflow.png)

1. **Plan**: Forces Claude to brainstorm and write a `plan.md` before coding.
2. **Execute**: Enforces step-by-step implementation with security and UI/UX checks.
3. **Verify**: Stops Claude from declaring success until tests/linters pass.
4. **Handoff**: Automatically generates a `handoff.md` to preserve context.

## 📦 Installation

### Option 1: Claude Code Plugin Marketplace (Recommended)
```bash
/plugin marketplace add kjhk3082/master-assistant-skill
/plugin install master-assistant-skill
```

### Option 2: Manual Installation
Clone this repository into your global or project-specific skills directory:
```bash
# Global installation
git clone https://github.com/kjhk3082/master-assistant-skill.git ~/.claude/skills/master-assistant

# Project-specific installation
git clone https://github.com/kjhk3082/master-assistant-skill.git .claude/skills/master-assistant
```

## 🛠️ What's Included?

This repository contains a suite of specialized skills that work together:

| Skill | Automatic Trigger Condition | Purpose |
|-------|---------------------------|---------|
| `master-assistant` | **Always active** | Orchestrates the workflow and routes to sub-skills. |
| `brainstorming` | New feature/idea | Asks clarifying questions and gets design approval. |
| `planning` | Approved design | Creates a step-by-step `plan.md`. |
| `debugging` | Error or bug | Enforces a 4-phase root cause analysis before fixing. |
| `ui-ux` | Frontend changes | Enforces design system, accessibility, and 4px grid. |
| `security` | Backend/Data changes | Enforces input validation and secure coding practices. |
| `review` | Completed steps | Verifies code quality and test coverage. |

## 💡 Real-World Example

Here is how Claude Code behaves **before** and **after** installing this skill:

![Before and After Example](assets/example-before-after.png)

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details on how to submit pull requests, report issues, or suggest new skills.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⌨️ Custom Slash Commands

You can also trigger these skills manually using the included slash commands:
(포함된 슬래시 커맨드를 사용하여 수동으로 스킬을 트리거할 수도 있습니다:)

| Command | Description |
|---------|-------------|
| `/m-brainstorming` | Start brainstorming process (브레인스토밍 시작) |
| `/m-planning` | Create implementation plan (구현 계획 작성) |
| `/m-debugging` | Start systematic debugging (체계적인 디버깅 시작) |
| `/m-ui-ux` | Apply UI/UX guidelines (UI/UX 가이드라인 적용) |
| `/m-security` | Apply secure coding practices (보안 코딩 관행 적용) |
| `/m-review` | Review code changes (코드 변경 사항 검토) |
