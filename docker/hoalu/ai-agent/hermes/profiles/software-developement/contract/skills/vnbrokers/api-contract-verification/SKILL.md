---
name: api-contract-verification
description: Verify Hoalulab broker and SDK contracts. Use for OpenAPI, AsyncAPI, HTTP, WebSocket, authentication, schema, compatibility, and contract-test analysis involving DNSE, FHSC, SSI, TCBS, or other supported providers.
---

# API Contract Verification

1. Query the configured Hoalulab documentation MCP for the specific broker and operation.
2. Inspect formal OpenAPI, AsyncAPI, schemas, fixtures, and relevant implementation when available.
3. Record exact method, path, parameters, headers, authentication, request shape, response shape, errors, and lifecycle rules.
4. Distinguish documented facts, observed provider behavior, implementation behavior, and unresolved conflicts.
5. Apply evidence precedence: verified provider behavior, formal contract, maintained MCP documentation, implementation, then examples and tests.
6. Identify compatibility and breaking-change risks.
7. Propose contract tests around externally observable behavior, including failure cases.
8. Cite the exact source used in the handoff.

Do not modify production SDK behavior. Never infer one broker's authentication or signing scheme from another broker.