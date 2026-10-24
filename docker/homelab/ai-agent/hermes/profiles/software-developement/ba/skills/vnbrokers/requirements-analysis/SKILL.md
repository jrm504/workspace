---
name: requirements-analysis
description: Produce implementation-neutral Hoalulab software requirements. Use when translating product goals, broker workflows, or stakeholder requests into scenarios, business rules, edge cases, constraints, and testable acceptance criteria.
---

# Requirements Analysis

1. Identify actors, goals, triggers, preconditions, and externally observable outcomes.
2. Separate confirmed facts, assumptions, decisions, and open questions.
3. Describe the primary workflow and failure, boundary, permission, timeout, retry, and concurrency scenarios relevant to the request.
4. Express business rules without prescribing classes, modules, libraries, or architecture.
5. Write acceptance criteria as observable Given/When/Then scenarios where useful.
6. Define explicit non-goals and compatibility constraints.
7. Trace every acceptance criterion to a stated user or business outcome.

Read project documentation and relevant source only to understand existing behavior. Do not execute code or modify production files.