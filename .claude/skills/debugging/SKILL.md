---
name: debugging
description: Systematic, evidence-driven debugging workflow — reproduce, isolate, root-cause, fix, and prevent regression. Use when investigating a bug, failure, crash, or regression.
---

# Systematic Debugging

A disciplined, evidence-driven debugging workflow.

## 1. Reproduce

- Establish a reliable, minimal reproduction.
- Capture exact inputs, environment, and version.
- Note frequency (always / intermittent).

## 2. Isolate

- Narrow the failure to the smallest scope.
- Bisect changes (`git bisect`) when a regression is suspected.
- Form competing hypotheses; rank them by likelihood.

## 3. Root Cause

- Trace the actual cause, not the symptom.
- Validate the hypothesis with evidence (logs, traces, state).
- Confirm you can explain why it fails every time.

## 4. Fix

- Apply the minimal correct fix at the root cause.
- Avoid masking symptoms or adding defensive noise.
- Consider side effects and edge cases.

## 5. Prevent Regression

- Add a test that fails before the fix and passes after.
- Add observability (logs / metrics) if the issue was hard to detect.
- Document the root cause and the fix.

## Output

- Reproduction steps
- Root cause
- Fix
- Regression test
- Severity (S0–S3)
