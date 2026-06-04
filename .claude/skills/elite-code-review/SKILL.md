---
name: elite-code-review
description: Principal-engineer production-grade code review across correctness, memory safety, undefined behavior, concurrency, security, reliability, performance, scalability, maintainability, observability, testing, and architecture. Includes C and C++ specific checks. Use when reviewing a PR, diff, or code change and you want a thorough, severity-rated (S0-S3) review.
---

# Elite Code Review v2

Act as a Principal Engineer performing production-grade review.

Review Order:

1. Correctness
2. Memory Safety
3. Undefined Behavior
4. Concurrency
5. Security
6. Reliability
7. Performance
8. Scalability
9. Maintainability
10. Observability
11. Testing
12. Architecture

---

## Correctness

Review:

* logic errors
* edge cases
* null handling
* state transitions
* transaction boundaries
* pagination correctness
* timezone correctness

---

## Memory Safety

Review:

* memory leaks
* double free
* use-after-free
* dangling pointers
* invalid ownership transfer
* stack lifetime violations
* heap corruption risks
* buffer overrun
* buffer underrun

Severity:

S1 minimum

---

## Undefined Behavior

Review:

* out-of-bounds access
* signed integer overflow
* invalid pointer arithmetic
* null dereference
* strict aliasing violations
* alignment issues
* uninitialized memory reads
* invalid casts
* sequence point violations

Assume:

* C11
* C17
* C++17+
* compiler optimizations enabled

Severity:

S1 minimum

---

## Concurrency

Review:

* race conditions
* deadlocks
* lock inversion
* ABA issues
* atomic misuse
* memory ordering issues
* thread safety
* signal safety

Assume multi-threaded execution.

---

## Security

Review:

* SQL injection
* command injection
* path traversal
* SSRF
* XSS
* CSRF
* auth bypass
* secret leakage
* insecure deserialization

---

## Reliability

Review:

* timeout handling
* retry strategy
* circuit breaker usage
* error propagation
* failure recovery
* idempotency

---

## Performance

Review:

* N+1 queries
* unnecessary allocations
* excessive copies
* lock contention
* cache inefficiencies
* hot-path bottlenecks

---

## Scalability

Review:

* bottlenecks
* queue design
* caching strategy
* distributed system concerns
* horizontal scaling

---

## Maintainability

Review:

* duplication
* coupling
* cohesion
* abstraction quality
* naming consistency

---

## Observability

Review:

* logging
* metrics
* tracing
* alertability

---

## Testing

Review:

* unit coverage
* integration coverage
* regression coverage
* edge-case coverage

---

## Architecture

Review:

* separation of concerns
* dependency direction
* domain boundaries
* long-term maintainability

---

## C-Specific Review

Review:

* ownership tracking
* malloc/free pairing
* pointer lifetime
* integer overflow
* integer underflow
* sign conversion
* truncation
* ABI compatibility
* structure packing assumptions

---

## C++-Specific Review

Review:

* Rule of Three
* Rule of Five
* Rule of Zero
* RAII correctness
* move semantics
* copy semantics
* exception safety
* smart pointer misuse
* object slicing
* virtual destructor requirements

---

## Severity Levels

### S0

Production outage, data corruption, or system crash.

### S1

Security vulnerability, memory corruption, UB, race condition.

### S2

Major performance, reliability, or maintainability issue.

### S3

Minor improvement suggestion.

---

## Final Verdict

One of:

* APPROVE
* APPROVE_WITH_COMMENTS
* REQUEST_CHANGES

Never approve code containing S0 or S1 findings.
