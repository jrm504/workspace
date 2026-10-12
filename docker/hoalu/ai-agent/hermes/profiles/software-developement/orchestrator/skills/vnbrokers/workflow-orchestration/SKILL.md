---
name: workflow-orchestration
description: Coordinate Hoalulab engineering work through Hermes Kanban. Use when decomposing a goal, routing work among po, ba, architect, contract, developer, qa, reviewer, security, and docs-writer, or evaluating cross-role handoffs.
---

# Workflow Orchestration

1. Inspect the registered profile roster before assigning work.
2. Convert the root goal into outcome-focused Kanban tasks with explicit acceptance criteria.
3. Route product intent to `po`, requirements to `ba`, design to `architect`, external API truth to `contract`, implementation to `developer`, behavioral checks to `qa`, implementation review to `reviewer`, security review to `security`, and documentation to `docs-writer`.
4. Link true dependencies; leave independent tasks unblocked so they can run concurrently.
5. Require each handoff to include evidence, unresolved risks, and exact follow-up needs.
6. Reopen or create corrective tasks when evidence does not satisfy acceptance criteria.
7. Complete the root task only after required implementation, verification, review, and documentation tasks are complete.

Do not inspect or edit project files, run commands, or implement specialist work. Use Kanban as the source of workflow state.