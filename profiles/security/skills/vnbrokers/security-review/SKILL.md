---
name: security-review
description: Review VNBrokers applications and broker integrations for security defects. Use for authentication, authorization, signing, secrets, TLS, PII, input validation, logging, dependency risk, and trust-boundary analysis.
---

# Security Review

1. Map assets, actors, entry points, trust boundaries, and attacker-controlled inputs.
2. Inspect authentication, authorization, token lifecycle, request signing, replay protection, TLS verification, secret storage, and sensitive logging.
3. Check broker-specific contract details against authoritative documentation; do not generalize between providers.
4. Review input validation, deserialization, file paths, command execution, SSRF, injection, dependency provenance, and failure handling where relevant.
5. Validate exploitability with the least invasive safe method; never use real trading actions or expose credentials.
6. Report each finding with severity, affected file and line, attack preconditions, impact, evidence, and remediation.
7. Separate confirmed vulnerabilities from hardening suggestions and unresolved verification gaps.

Do not modify production implementation by default. Never include secrets, tokens, OTPs, account identifiers, or raw sensitive payloads in findings.