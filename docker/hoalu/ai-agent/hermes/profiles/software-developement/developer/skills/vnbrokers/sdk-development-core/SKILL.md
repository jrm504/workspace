---
name: sdk-development-core
description: Cross-language implementation workflow for production client SDK code.
version: 1.0.0
metadata:
  hermes:
    tags: [development, sdk, implementation, api-client]
    category: software-development
---

# SDK Development Core

## When to use

Use this skill for production implementation work in a client SDK regardless
of language.

## Procedure

1. Read repository instructions and the assigned acceptance criteria.
2. Inspect neighboring implementations and public interfaces.
3. Identify protocol, compatibility, error, cancellation, and lifecycle
   constraints.
4. Implement the smallest coherent production change.
5. Run the repository's formatter/build/static checks for the changed area.
6. Run relevant existing tests.
7. Review the diff and hand off with exact evidence.

## API compatibility

Treat these as compatibility-sensitive:

- exported/public names
- method signatures
- request paths and parameter names
- serialization shapes
- enum/string values
- error categories
- pagination behavior
- websocket event/subscription semantics

Do not change a public contract merely to simplify implementation.

## HTTP clients

Preserve:

- method and path
- query encoding
- required headers
- authentication/signing boundaries
- body serialization
- status/error mapping
- response cleanup
- timeout/cancellation behavior

Keep transport concerns separated from domain mapping when the repository
already follows that pattern.

## Realtime clients

Model lifecycle explicitly:

- connect
- authenticate
- subscribe
- receive
- unsubscribe
- reconnect
- restore active subscriptions
- close/cancel

Avoid duplicate callbacks, leaked goroutines/tasks, unbounded retries, and
arbitrary sleeps.

## Error handling

Do not silently swallow provider or transport errors.

Preserve enough cause/context for callers and testers to distinguish:

- validation errors
- authentication/authorization failures
- provider/API failures
- transport failures
- cancellation/timeouts
- malformed payloads

## Test handoff

The developer runs relevant existing tests but the tester owns comprehensive
automated-test implementation.

Provide the tester with important state transitions, protocol boundaries, and
failure paths that deserve independent coverage.
