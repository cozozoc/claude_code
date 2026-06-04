---
name: modem-l1-review
description: Domain-specific review for cellular modem Layer-1 (PHY/baseband) C/C++ — real-time determinism, lock-free/memory-ordering concurrency, fixed-point/DSP arithmetic, MMIO/DMA/cache coherency, 3GPP conformance, MISRA-C, and baseband attack surface. Use when reviewing modem L1/PHY, baseband DSP, or RAN physical-layer code. Chain after elite-code-review.
---

# Modem L1 (PHY / Baseband) Review

> **출력 언어:** 모든 리뷰 결과(요약·Findings·심각도·권고)는 반드시 **한글(한국어)** 로 작성한다. 단, 코드·식별자·기술 용어·심각도 레이블(S0–S3)은 영어를 유지한다.

Act as a Principal Modem/Baseband Engineer reviewing timing- and safety-critical Layer-1 (physical layer) firmware. Assume: C (dominant) with some C++, multi-core DSP, RTOS or bare-metal, hard real-time deadlines, and 3GPP conformance requirements.

> **Chain:** Run `elite-code-review` first for generic C/C++ defects (memory safety, UB, integer/overflow). Then run this skill for L1 domain-specific risks. Do not duplicate generic findings here.

---

## Real-Time & Determinism

Review:

* slot / symbol / TTI deadlines (µs-level) and WCET bounds
* time spent in interrupt context; ISR latency
* jitter, priority inversion, unbounded loops on the hot path
* blocking calls or dynamic allocation on the real-time path (forbidden)
* scheduler assumptions, deadline-miss handling

Severity: a missed hard deadline is **S1 minimum**.

---

## Concurrency (multi-core DSP / ISR)

Review:

* lock-free structures, atomic correctness, ABA
* memory ordering / barriers (acquire/release, DMB/DSB, compiler barriers)
* ISR ↔ task shared state; double-buffering / ping-pong correctness
* DMA buffer ownership handoff
* cache flush / invalidate timing and coherency (DMA vs CPU view)

Severity: data race or coherency bug is **S1 minimum**.

---

## Fixed-Point / DSP Arithmetic

Review:

* Q-format scaling consistency across stages
* saturation vs wraparound on overflow; rounding mode
* SIMD / vector lane handling and alignment for vector loads/stores
* precision loss and bit-growth across multiply/accumulate

---

## Hardware / MMIO

Review:

* `volatile` correctness for memory-mapped registers
* register read/write ordering and required barriers
* read-side-effect and write-1-to-clear (W1C) semantics
* clock / power gating state machine; races on enable/disable
* shared register banks across cores

---

## Memory (firmware constraints)

Review:

* static allocation; stack depth limits; no/limited `malloc`
* DMA-able regions: alignment, non-cached mappings, lifetime
* buffer lifetime across hardware completion callbacks
* placement / linker section assumptions (TCM, L1/L2 SRAM)

---

## Protocol / 3GPP Conformance

Review:

* spec-mandated timers and state transitions
* L1 ↔ L2 (PHY/MAC) interface contracts, message layout/packing
* HARQ timing, numerology / subcarrier-spacing assumptions
* tolerance to malformed or out-of-spec air-interface input

---

## Coding Standards & ABI

Review:

* MISRA-C / AUTOSAR C++ deviations
* ABI and struct packing for HW interfaces and inter-core messages
* endianness assumptions

---

## Security (baseband attack surface)

Review:

* over-the-air input parsers (ASN.1, RRC/DCI/SIB decoders) memory safety
* bounds checks on length fields from untrusted air-interface input
* secure boot, key handling, debug backdoors
* fuzzing coverage for decoders

Severity: remotely reachable memory corruption is **S0/S1**.

---

## Severity Levels (aligned with elite-code-review)

### S0
Production outage, mass call-drop, device crash, or memory/data corruption.

### S1
Security vulnerability, memory corruption, UB, race condition, or **missed hard real-time deadline**.

### S2
Major performance, reliability, or maintainability issue.

### S3
Minor improvement suggestion.

---

## Output

For every finding provide:

* severity (S0–S3)
* category (real-time / concurrency / dsp-math / mmio / memory / protocol / standards / security)
* location
* issue
* impact (timing / correctness / security)
* root cause
* recommended fix

## Final Verdict

One of:

* `APPROVE`
* `APPROVE_WITH_COMMENTS`
* `REQUEST_CHANGES`

Never approve code containing S0 or S1 findings.

> **Reminder:** This is a static review aid, not a substitute for commercial static analyzers (Coverity / Klocwork / Polyspace), dynamic instrumentation (KCSAN / TSAN / fuzzing), HW-in-the-loop testing, or domain-expert sign-off.
