---
name: security
description: "You MUST use this when writing or reviewing code that handles user input, authentication, authorization, or sensitive data. Enforces secure coding practices."
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
