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
