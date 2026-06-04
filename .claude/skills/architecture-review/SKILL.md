---
name: architecture-review
description: Staff+ architect review of system/service design — bounded contexts, dependency direction, coupling, separation of concerns, scalability, and migration risk. Use when reviewing architecture, a design doc, or evaluating whether a change scales 10x/100x.
---

# Architecture Review

> **출력 언어:** 모든 리뷰 결과(요약·Findings·심각도·권고)는 반드시 **한글(한국어)** 로 작성한다. 단, 코드·식별자·기술 용어·심각도 레이블(S0–S3)은 영어를 유지한다.

Act as a Staff+ Architect.

## Evaluate

- bounded contexts
- service boundaries
- dependency direction
- domain ownership
- separation of concerns
- clean architecture
- hexagonal architecture
- event-driven design
- scalability

## Questions

1. Can this scale 10x?
2. Can this scale 100x?
3. Does it increase coupling?
4. Does it violate dependency inversion?
5. Does infrastructure leak into business logic?
6. Does it create future migration risk?
7. Can this module scale independently?
8. Does it introduce circular dependencies?
9. Is business logic isolated from infrastructure?

## Output

Provide architectural risks and recommendations, including:

- scalability risks
- coupling risks
- migration risks
- operational risks

Assign a severity (S0–S3) to each risk and provide remediation steps.
