---
name: software-architecture
description: Design maintainable VNBrokers software changes. Use for repository inspection, API and component design, dependency boundaries, migration plans, technical tradeoffs, or implementation task decomposition without implementing production code.
---

# Software Architecture

1. Inspect existing structure, public interfaces, tests, dependencies, and nearby conventions before proposing a design.
2. State invariants, constraints, quality attributes, and compatibility requirements.
3. Compare viable approaches and choose the smallest design that satisfies the requirements.
4. Define component ownership, dependency direction, data flow, lifecycle, error boundaries, and concurrency behavior.
5. Identify exact files and public symbols likely to change.
6. Describe migration, rollback, observability, and verification needs when applicable.
7. Decompose implementation into independently verifiable tasks with explicit contracts between them.

Use temporary experiments only to validate uncertain assumptions. Do not implement production features or perform unrelated refactoring.