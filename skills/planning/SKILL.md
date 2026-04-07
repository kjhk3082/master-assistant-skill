---
name: planning
description: "[EN] You MUST use this after brainstorming or when you have a clear design/spec but before writing any code. Breaks down work into actionable, verifiable steps. [KO] 브레인스토밍 후 또는 명확한 설계/사양이 있지만 코드를 작성하기 전에 반드시 사용해야 합니다. 작업을 실행 가능하고 검증 가능한 단계로 나눕니다."
---

# Writing Implementation Plans

Turn approved designs into actionable implementation plans.

<HARD-GATE>
Do NOT write any code until the user has approved the implementation plan.
</HARD-GATE>

## Checklist

1. **Review Design** - Read the approved design document
2. **Break Down Work** - Create a step-by-step plan in `plan.md`
3. **Include Verification** - Every step MUST have a way to verify it works (tests, visual check, etc.)
4. **Get Approval** - Present the plan to the user and ask for approval
5. **Execute** - Once approved, use the `EnterPlanMode` tool (if available) or proceed step-by-step

## Plan Format

Your `plan.md` MUST follow this structure:

```markdown
# Implementation Plan: [Feature Name]

## Prerequisites
- [ ] Check environment
- [ ] Install dependencies

## Steps
1. [ ] **[Component/Module]**: [Brief description]
   - Files to modify: `path/to/file`
   - Verification: Run `npm test` or specific command

2. [ ] **[Next Component]**: ...
```
