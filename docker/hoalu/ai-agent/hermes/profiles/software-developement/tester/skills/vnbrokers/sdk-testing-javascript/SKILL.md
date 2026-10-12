---
name: sdk-testing-javascript
description: Implement and run JavaScript/TypeScript SDK tests using the repository's existing Vitest, Jest, Node test runner, or equivalent setup.
version: 1.0.0
metadata:
  hermes:
    tags: [testing, javascript, typescript, nodejs, sdk]
    category: software-development
---

# JavaScript and TypeScript SDK Testing

## Detect the project first

Inspect:
- `package.json`
- package-manager lockfile
- test config (`vitest`, `jest`, Node test runner, etc.)
- `tsconfig.json`
- existing test directories
- CI workflows

Use the repository's package manager and scripts. Prefer `npm/pnpm/yarn/bun <script>` defined by the project over hard-coded runner commands.

## Common checks

Typical project-defined commands may include:

```bash
npm test
npm run test
npm run test:coverage
npm run typecheck
npm run lint
```

Use the actual package manager and scripts present in the repository.

## JS/TS-specific cases

Test as relevant:
- Promise rejection/error mapping
- `AbortSignal` cancellation
- fetch/HTTP request construction
- ESM/CJS boundaries
- TypeScript runtime decoding assumptions
- optional/null/undefined behavior
- number precision constraints
- timers using fake/controlled clocks
- websocket event ordering, unsubscribe, reconnect, and cleanup

Restore mocked globals/timers after every test. Avoid tests that depend on global mutation leaking across cases.

## Verification

Run the smallest affected test target, then the project test script and relevant type/lint checks.
