---
name: security-audit
description: Full OWASP-based security audit — authentication, authorization, secrets management, input validation, injection (SQL/command/SSRF/path traversal), insecure deserialization, and unsafe logging. Use when reviewing code for security vulnerabilities or running a security pass on a PR.
---

# Security Audit

Perform a full OWASP review.

## Threat Model

- authentication
- authorization
- data protection
- secrets management
- input validation
- session management
- logging practices

## Always Check

- OWASP Top 10
- hardcoded credentials
- token leakage
- privilege escalation
- insecure defaults
- unsafe deserialization
- SSRF / command injection / path traversal
- unsafe logging (PII / secrets in logs)

## Output

Output only findings. For each finding provide:

- severity (S0–S3)
- category
- location
- issue
- impact
- recommended fix
