---
name: sdk-development-javascript
description: Implement production JavaScript and TypeScript SDK code using the repository's existing Node, package-manager, typing, and async conventions.
version: 1.0.0
metadata:
  hermes:
    tags: [development, javascript, typescript, nodejs, sdk]
    category: software-development
---

# JavaScript and TypeScript SDK Development

## Detect the project first

Inspect:

- `package.json`
- package-manager lockfile
- `tsconfig.json`
- ESM/CJS configuration
- formatter/linter configuration
- existing client and error patterns
- CI scripts

Use the repository's existing package manager and scripts.

## Implementation concerns

Preserve as applicable:

- exported TypeScript API compatibility
- Promise rejection semantics
- `AbortSignal` cancellation
- fetch/HTTP client conventions
- ESM/CJS packaging behavior
- runtime validation assumptions
- `null` vs `undefined`
- JavaScript number precision constraints
- timer ownership and cleanup
- websocket listener/subscription cleanup

Avoid mutating globals for production behavior.

Do not create retry loops without bounded policy and cancellation.

## Typical validation

Prefer project scripts, for example:

```bash
npm run build
npm test
npm run typecheck
npm run lint
```

Use `pnpm`, `yarn`, or `bun` instead when that is the repository's established
toolchain.
