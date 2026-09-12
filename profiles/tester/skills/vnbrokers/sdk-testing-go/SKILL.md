---
name: sdk-testing-go
description: Implement and run Go SDK tests using testing, httptest, race detection, and the repository's established conventions.
version: 1.0.0
metadata:
  hermes:
    tags: [testing, go, golang, sdk]
    category: software-development
---

# Go SDK Testing

## Detect the project first

Inspect:
- `go.mod`
- package-local `*_test.go`
- existing use of `testify`, `gomock`, or other helpers
- CI test commands
- build tags

Prefer standard `testing` and existing project conventions.

## Common commands

```bash
go test ./path/to/package
go test ./...
go test -race ./...
go test -coverprofile=coverage.out ./...
go tool cover -func=coverage.out
```

Run `-race` when concurrency is relevant and the environment supports it.

## Go-specific cases

Test as relevant:
- context cancellation/deadlines
- HTTP request construction with `httptest`
- `io.Closer`/body cleanup
- JSON optional/pointer fields
- numeric conversion
- error wrapping and `errors.Is` / `errors.As`
- goroutine lifecycle and channel closure
- websocket reconnect/subscription state
- concurrent client safety

Avoid goroutine leaks and timing-sensitive sleeps. Prefer channels, contexts, wait groups, and observable synchronization.

## Verification

Run the focused package tests first, then `go test ./...`; add race and coverage runs where they provide useful evidence.
