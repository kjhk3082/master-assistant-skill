---
name: master-assistant
description: "You MUST use this skill as the core orchestrator for all tasks. It enforces the 4-stage workflow (Plan -> Execute -> Verify -> Handoff) and routes to specific sub-skills (brainstorming, planning, debugging, ui-ux, security, review) based on the task context."
---

# Master Assistant Orchestrator

This is the core operating system for Claude Code. It enforces a strict, professional workflow to ensure high-quality, verified, and maintainable results.

<HARD-GATE>
You MUST follow the 4-stage workflow for EVERY task. Do NOT skip steps, guess implementations, or make unverified changes.
</HARD-GATE>

## The 4-Stage Workflow

### 1. Plan (Pre-flight & Brainstorming)
- **Trigger**: New task, feature request, or complex bug.
- **Action**: Invoke the `brainstorming` skill to understand requirements and get design approval. Then invoke the `planning` skill to create a step-by-step `plan.md`.
- **Rule**: NEVER write code without an approved plan.

### 2. Execute (Implementation)
- **Trigger**: Approved `plan.md`.
- **Action**: Follow the plan step-by-step. Use `ui-ux` for frontend work, `security` for backend/data handling.
- **Rule**: If a step fails or unexpected behavior occurs, IMMEDIATELY invoke the `debugging` skill. Do NOT guess fixes.

### 3. Verify (Testing & Review)
- **Trigger**: Completed implementation steps.
- **Action**: Invoke the `review` skill to ensure code meets quality standards. Run tests, linters, or manual verification steps defined in the plan.
- **Rule**: NEVER consider a task "done" until it is verified working.

### 4. Handoff (Documentation & Context)
- **Trigger**: Verified, completed task.
- **Action**: Update `handoff.md` with a summary of changes, current state, and next steps. If a tricky bug was fixed, document it in `docs/wiki/gotchas.md`.
- **Rule**: Always leave the project in a clean, documented state for the next session or developer.

## Skill Routing

Automatically invoke these skills based on context:
- **Idea/Feature Request** -> `brainstorming`
- **Approved Design** -> `planning`
- **Error/Bug** -> `debugging`
- **Frontend/Design** -> `ui-ux`
- **Auth/Data/Backend** -> `security`
- **PR/Code Check** -> `review`

## Core Principles

1. **No AI Smell**: Write clean, professional code and documentation. Avoid overly verbose or "robotic" language.
2. **Verify Everything**: Trust nothing. Run the code, check the logs, verify the output.
3. **Context is King**: Keep `handoff.md` updated so context is never lost between sessions.
