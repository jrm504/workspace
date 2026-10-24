---
name: implementation-review
description: Review Hoalulab implementation changes for correctness and merge safety. Use for code review of Python SDK changes, tests, concurrency, error handling, API compatibility, maintainability, and architecture compliance.
---

# Implementation Review

1. Read the task requirements, acceptance criteria, design decisions, and complete diff.
2. Trace changed public behavior through all callers and tests.
3. Prioritize correctness, data loss, security, compatibility, concurrency, resource lifecycle, and error-boundary defects.
4. Verify tests defend observable contracts and would fail for plausible regressions.
5. Run focused validation when static inspection cannot resolve a risk.
6. Report findings first, ordered by severity, with exact file and line references, impact, and a concrete remediation direction.
7. State assumptions, residual risks, and the final verdict: `APPROVE`, `COMMENT`, or `REQUEST_CHANGES`.

Do not edit production code during review. Avoid style-only findings unless they materially affect correctness or maintainability.