---
name: sdk-development-dotnet
description: Implement production C# and .NET SDK code using the repository's existing async, HttpClient, serialization, nullable, and packaging conventions.
version: 1.0.0
metadata:
  hermes:
    tags: [development, dotnet, csharp, sdk]
    category: software-development
---

# .NET SDK Development

## Detect the project first

Inspect:

- `.sln` / `.slnx`
- project files
- target frameworks
- nullable configuration
- analyzer/style configuration
- package conventions
- existing `HttpClient` and dependency-injection patterns
- CI commands

## Implementation concerns

Preserve as applicable:

- public API and binary/source compatibility expectations
- `async`/`await` behavior
- `CancellationToken` propagation
- `HttpClient` lifetime conventions
- `IDisposable` / `IAsyncDisposable` cleanup
- nullable reference semantics
- `System.Text.Json` configuration
- `decimal` vs floating-point semantics
- typed API exception behavior
- websocket lifecycle and cancellation

Avoid sync-over-async patterns such as `.Result` or `.Wait()` in asynchronous
code paths.

Do not create unmanaged `HttpClient` lifetimes when the repository already has
a factory/client ownership convention.

## Typical validation

```bash
dotnet build
dotnet test
dotnet format --verify-no-changes
```

Run only checks supported by the repository/tooling.
