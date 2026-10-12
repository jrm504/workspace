---
name: sdk-development-python
description: Implement production Python SDK code using the repository's existing packaging, typing, async, and client conventions.
version: 1.0.0
metadata:
  hermes:
    tags: [development, python, sdk, asyncio]
    category: software-development
---

# Python SDK Development

## Detect the project first

Inspect:

- `pyproject.toml`
- lockfiles
- package layout
- typing configuration
- formatter/linter configuration
- existing sync/async client patterns
- CI commands

Use the existing dependency manager and style.

## Implementation concerns

Preserve as applicable:

- sync vs async API symmetry
- `asyncio` cancellation semantics
- context-manager cleanup
- type hints and public typing compatibility
- dataclass/Pydantic/model conventions already in use
- optional/null handling
- `Decimal` vs `float` semantics where precision matters
- timezone-aware datetime behavior
- exception chaining and provider error mapping

Do not block the event loop with synchronous I/O inside async APIs.

Do not create background tasks without a clear ownership and cancellation
strategy.

## Typical validation

Use the project's own scripts/configuration. Common commands may include:

```bash
python -m compileall <package>
pytest <relevant-target>
ruff check .
mypy <package>
```

Only run tools configured or available in the repository.
