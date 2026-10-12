---
name: sdk-testing-python
description: Implement and run Python SDK tests using the repository's existing pytest/unittest and coverage conventions.
version: 1.0.0
metadata:
  hermes:
    tags: [testing, python, pytest, unittest, sdk]
    category: software-development
---

# Python SDK Testing

## Detect the project first

Inspect:
- `pyproject.toml`
- `pytest.ini`
- `tox.ini`
- `setup.cfg`
- `tests/`
- lockfiles and CI workflows

Use the existing runner and dependency manager. Do not introduce pytest if the repository intentionally uses `unittest`, and do not replace an existing mocking library without need.

## Common targets

For pytest-based repositories, typical commands are:

```bash
pytest path/to/test_file.py -q
pytest -q
pytest --cov=<package> --cov-report=term-missing
```

Only use flags/plugins already available in the project.

## Python-specific cases

Test as relevant:
- sync and async clients
- context managers and resource cleanup
- `asyncio` cancellation
- timeout propagation
- dataclass/Pydantic/model mapping
- optional values and malformed payloads
- decimal/float/int conversion
- timezone-aware timestamps
- exception chaining and API error mapping

For HTTP integrations, prefer the project's current approach such as an in-process server, transport mock, `respx`, `responses`, or another existing dependency.

For async tests, await observable conditions instead of sleeping.

## Verification

Run the narrow test, then the relevant full suite and the repository's lint/type checks when required.
