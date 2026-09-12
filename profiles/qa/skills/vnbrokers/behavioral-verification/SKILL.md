---
name: behavioral-verification
description: Verify VNBrokers software behavior against acceptance criteria. Use when reproducing defects, exercising broker integrations, testing edge cases and regressions, or producing an evidence-based QA verdict without fixing production code.
---

# Behavioral Verification

1. Translate each acceptance criterion into an observable check.
2. Reproduce reported defects before assessing a fix when a runnable reproduction exists.
3. Exercise the real changed path at the narrowest useful layer; use deterministic fixtures for external providers unless a safe live check is explicitly available.
4. Cover success, invalid input, authorization failure, provider failure, timeout, retry, state transition, and concurrency cases that are relevant to the change.
5. Distinguish test-environment evidence from live-provider evidence.
6. Report commands or scenarios run, observed results, environment constraints, and residual risk.
7. Return `PASS`, `FAIL`, or `BLOCKED`; include a minimal reproducible finding for every failure.

QA may create or update test artifacts only when the task permits. Do not modify production implementation to make a failing check pass.