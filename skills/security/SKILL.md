---
name: security
description: "[EN] You MUST use this when writing or reviewing code that handles user input, authentication, authorization, or sensitive data. Enforces secure coding practices. [KO] 사용자 입력, 인증, 권한 부여 또는 민감한 데이터를 처리하는 코드를 작성하거나 검토할 때 반드시 사용해야 합니다. 안전한 코딩 관행을 강제합니다."
---

# Secure Coding Practices

Guidelines for writing secure code and preventing common vulnerabilities.

<HARD-GATE>
Do NOT trust user input. Always validate, sanitize, and escape data before processing, storing, or displaying it.
</HARD-GATE>

## Core Security Principles

1. **Defense in Depth**: Implement multiple layers of security controls
2. **Least Privilege**: Grant only the minimum necessary permissions
3. **Fail Securely**: Handle errors gracefully without exposing sensitive information
4. **Keep It Simple**: Avoid unnecessary complexity that can introduce vulnerabilities

## Implementation Checklist

- [ ] Validate all user input (type, length, format, range)
- [ ] Use parameterized queries or ORMs to prevent SQL injection
- [ ] Escape output to prevent Cross-Site Scripting (XSS)
- [ ] Implement proper authentication and authorization checks
- [ ] Securely store and transmit sensitive data (encryption, hashing)
- [ ] Avoid hardcoding secrets or credentials in source code
