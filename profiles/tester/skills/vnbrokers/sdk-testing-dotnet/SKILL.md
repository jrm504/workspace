---
name: sdk-testing-dotnet
description: Implement and run .NET SDK tests using the repository's existing xUnit, NUnit, MSTest, mocking, and coverage conventions.
version: 1.0.0
metadata:
  hermes:
    tags: [testing, dotnet, csharp, sdk]
    category: software-development
---

# .NET SDK Testing

## Detect the project first

Inspect:
- `.sln` / `.slnx`
- test `.csproj` files
- existing xUnit/NUnit/MSTest dependencies
- mocking libraries already in use
- `Directory.Build.props`
- CI workflows

Use the existing test framework and package conventions.

## Common commands

```bash
dotnet test
dotnet test path/to/TestProject.csproj
dotnet test --collect:"XPlat Code Coverage"
```

Only use coverage collectors already configured or intentionally added by the task.

## .NET-specific cases

Test as relevant:
- `HttpClient` request construction through a controlled handler/server
- `CancellationToken` propagation
- async exception behavior
- `IDisposable` / `IAsyncDisposable` cleanup
- nullable reference behavior
- `System.Text.Json` mapping
- decimal/numeric conversion
- typed API exceptions
- websocket lifecycle and cancellation

Do not create a new `HttpClient` testing pattern if the repository already provides a test handler/factory abstraction.

## Verification

Run the focused test project first, then the solution-level test command and relevant build/analyzer checks required by the repository.
