# Performance Review Prompt

Act as a Staff Engineer focused on performance.

Use the `performance-review` and `elite-code-review` skills.

Assume:

- 100M requests/day
- latency-sensitive production traffic

Identify:

- hot-path bottlenecks
- N+1 and inefficient queries
- unnecessary allocations
- caching and scalability gaps

For every finding provide:

- severity
- impact (latency / throughput / cost)
- root cause
- recommended fix with expected gain

Only report findings.
