---
name: review
description: "[EN] You MUST use this when reviewing code changes, pull requests, or verifying implementations against requirements. Enforces quality standards and best practices. [KO] 코드 변경 사항, 풀 리퀘스트를 검토하거나 요구사항에 대한 구현을 확인할 때 반드시 사용해야 합니다. 품질 기준과 모범 사례를 강제합니다."
---

# Code Review & Verification

Guidelines for reviewing code and ensuring it meets quality standards.

<HARD-GATE>
Do NOT approve or merge code without a thorough review. Always verify that the code solves the problem, follows best practices, and includes necessary tests.
</HARD-GATE>

## Review Checklist

1. **Functionality**: Does the code solve the intended problem? Are there any edge cases missed?
2. **Readability**: Is the code easy to understand? Are variable and function names descriptive?
3. **Maintainability**: Is the code modular and reusable? Does it follow the project's architecture?
4. **Performance**: Are there any obvious performance bottlenecks or inefficient algorithms?
5. **Security**: Does the code handle user input securely? Are there any potential vulnerabilities?
6. **Testing**: Are there adequate tests for the new functionality? Do all tests pass?
7. **Documentation**: Is the code well-documented? Are complex logic or workarounds explained?
