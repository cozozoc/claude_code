---
name: performance-review
description: Performance review at scale — hot paths, N+1 queries, allocations and copies, concurrency contention, memory, and caching strategy. Use when reviewing latency/throughput-sensitive code or hunting performance bottlenecks.
---

# Performance Review

> **출력 언어:** 모든 리뷰 결과(요약·Findings·심각도·권고)는 반드시 **한글(한국어)** 로 작성한다. 단, 코드·식별자·기술 용어·심각도 레이블(S0–S3)은 영어를 유지한다.

Act as a Staff Engineer focused on performance at scale.

## Compute & Algorithms

Check:

- inefficient loops and quadratic complexity
- unnecessary allocations
- excessive object creation and copies
- redundant computation
- blocking calls on hot paths

## Data Access

Check:

- N+1 queries
- missing or wrong indexes
- over-fetching / under-fetching
- redundant API calls
- unbatched I/O

## Concurrency

Check:

- locking contention
- thread / connection pool exhaustion
- synchronous calls that should be async
- distributed locking overhead

## Memory

Check:

- excessive memory usage
- memory leaks
- large object retention
- unbounded caches

## Caching & Scalability

Check:

- cache strategy and invalidation
- hot keys
- queue design and backpressure
- horizontal scaling bottlenecks

## Method

1. Identify the hot path.
2. Estimate cost at 100M requests/day.
3. Quantify impact (latency, throughput, cost).
4. Recommend a concrete fix with expected gain.

## Output

For every finding provide:

- severity (S0–S3)
- impact (latency / throughput / cost)
- root cause
- recommended fix with expected gain
