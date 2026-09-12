---
name: sdk-development-go
description: Implement production Go SDK code using idiomatic context, HTTP, concurrency, error, and package conventions.
version: 1.0.0
metadata:
  hermes:
    tags: [development, go, golang, sdk]
    category: software-development
---

# Go SDK Development

## Detect the project first

Inspect:

- `go.mod`
- package structure
- exported API conventions
- existing client/options patterns
- error conventions
- CI and lint configuration

Prefer existing repository patterns over introducing new abstractions.

## Implementation concerns

Preserve as applicable:

- `context.Context` cancellation and deadlines
- HTTP body cleanup
- request construction and query encoding
- pointer fields for optional JSON semantics
- wrapped errors compatible with `errors.Is` / `errors.As`
- goroutine lifecycle
- channel ownership and closure
- concurrency safety
- websocket reconnect and cancellation behavior

Never start an unbounded goroutine without a clear stop path.

Avoid holding locks across network I/O unless the design explicitly requires
it.

## Typical validation

```bash
gofmt -w <changed-go-files>
go test ./path/to/affected/package
go test ./...
go vet ./...
```

Use repository-specific lint commands when configured.
