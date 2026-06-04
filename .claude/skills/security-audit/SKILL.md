---
name: security-audit
description: Full OWASP-based security audit — authentication, authorization, secrets management, input validation, injection (SQL/command/SSRF/path traversal), insecure deserialization, and unsafe logging. Use when reviewing code for security vulnerabilities or running a security pass on a PR.
---

# Security Audit

> **출력 언어:** 모든 리뷰 결과(요약·Findings·심각도·권고)는 반드시 **한글(한국어)** 로 작성한다. 단, 코드·식별자·기술 용어·심각도 레이블(S0–S3)은 영어를 유지한다.

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
