---
name: sdk-testing-core
description: Cross-language workflow for designing and implementing automated tests for client SDKs.
version: 1.0.0
metadata:
  hermes:
    tags: [testing, sdk, unit-test, integration-test, contract-test, regression]
    category: software-development
---

# SDK Testing Core

## When to use

Use for test planning and implementation in any client SDK repository, especially when deciding between unit, integration, contract, and regression tests.

## Test-level selection

Choose the lowest level that can prove the behavior.

### Unit

Use for:
- validation
- mapping/transformation
- signing input construction
- serializers/deserializers
- error conversion
- retry decision logic
- state machines

Keep network and clock dependencies controlled.

### Integration

Use for:
- HTTP client + transport behavior
- generated/manual client boundaries
- middleware/interceptor chains
- websocket client behavior
- interaction with a local mock server or contract harness

Prefer a deterministic local service or in-process server.

### Contract

Use for:
- OpenAPI/AsyncAPI/schema compatibility
- request/response examples
- sanitized recorded fixtures
- broker/provider protocol behavior

A contract test should make protocol drift visible without requiring unrelated business logic.

### Regression

Every fixed defect should have a test that would fail if the defect returns, when practical.

## External systems

Default to no live external dependency.

Use live-provider testing only when the assigned task explicitly requires it. Never embed credentials, tokens, account identifiers, or other secrets in test files.

For trading SDKs, never place a real order as an incidental test action.

## Assertions

Assert behavior and protocol semantics rather than private implementation details.

Good assertions include:
- exact request method/path where protocol compatibility matters
- required headers and normalized values
- parsed domain values
- expected error type/category
- subscription state transitions
- emitted messages/events

Avoid:
- arbitrary object internals
- unstable timestamps without a controlled clock
- full snapshots when only a few semantic fields matter

## Flakiness controls

- No arbitrary sleep if a condition/event can be awaited.
- Use bounded deterministic timeouts.
- Isolate mutable global state.
- Make tests independent of execution order.
- Bind local servers to ephemeral ports where possible.
- Freeze or inject clocks when time affects behavior.

## Execution order

1. Run the smallest affected test target.
2. Run the affected package/module suite.
3. Run the repository suite required by its contribution/CI rules.
4. Run lint/type/static checks when test changes can affect them.

## Handoff

Report exact commands and actual results. Separate:
- test failures caused by the implementation
- test harness/environment failures
- untested scenarios
- independent QA recommendations
