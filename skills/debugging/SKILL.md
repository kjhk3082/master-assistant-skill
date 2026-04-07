---
name: debugging
description: "[EN] You MUST use this when investigating errors, bugs, or unexpected behavior. Provides a systematic approach to root cause analysis. [KO] 에러, 버그 또는 예기치 않은 동작을 조사할 때 반드시 사용해야 합니다. 근본 원인 분석에 대한 체계적인 접근 방식을 제공합니다."
---

# Systematic Debugging

A structured approach to finding and fixing bugs.

<HARD-GATE>
Do NOT guess or immediately change code when an error occurs. You MUST follow the systematic debugging process to find the root cause first.
</HARD-GATE>

## The 4-Phase Debugging Process

1. **Reproduce & Isolate**
   - Confirm the exact error message or behavior
   - Identify the minimal steps to reproduce

2. **Root Cause Tracing**
   - Trace the execution path backwards from the error
   - Add temporary logging if necessary
   - Formulate a hypothesis about the root cause

3. **Verify Hypothesis**
   - Test the hypothesis (e.g., by checking variable values)
   - Do NOT proceed to fixing until the hypothesis is confirmed

4. **Fix & Verify**
   - Apply the minimal necessary fix
   - Run tests or manually verify the fix resolves the issue without breaking other things
   - Document the fix in `docs/wiki/gotchas.md` if it's a recurring issue or tricky edge case
