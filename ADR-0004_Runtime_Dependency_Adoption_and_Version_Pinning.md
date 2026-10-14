# ADR-0004: Runtime Dependency Adoption and Version Pinning Policy

* **Status:** Accepted
* **Date:** 2026-10-14
* **Deciders:** Project Owner, System Architect, Security & Supply Chain Desk
* **Technical Domain:** Package Management, Supply Chain Security, Runtime Dependencies

---

## Context and Problem Statement

Gate M1 specification §1.3 and §6.1 (`AUDIT-45`) established a strict dependency minimization and version pinning rule, requiring exact version strings without semver range operators (`^` or `~`). The initial specification approved `json-canonicalize` pinned at `3.0.1`.

During Gate M2 (Market Feed Execution Engine & WebSocket Transport) and Gate M3 (Durable PostgreSQL Persistence & Concurrency), two additional runtime libraries were integrated into `package.json`:
1. `ws` for high-throughput loopback WebSocket order and market data transport.
2. `pg` for native PostgreSQL ACID transactions, row-level locking (`SELECT ... FOR UPDATE`), and connection pooling.

An independent audit (`ARGON-REV-POC001-20261014`, `F-07`) noted two compliance issues:
- `package.json` had temporarily introduced caret ranges (`^3.0.1`, `^8.19.0`, `^8.23.1`).
- The additions of `ws` and `pg` were documented in conformance reports rather than in a formal Architecture Decision Record.

## Decision Drivers

1. Supply chain determinism: Prevent silent updates from introducing breaking changes, security vulnerabilities, or subtle mathematical drift.
2. Compliance with Spec §1.3 and §6.1 (`AUDIT-45`).
3. Isolation of network and database drivers: restrict `ws` to loopback and `pg` to authorized persistent storage.

## Considered Options

* **Option 1 (Caret Semver Ranges):** Allow `^` ranges for non-cryptographic libraries to receive security patches automatically.
  - *Deficiency:* Non-deterministic builds across different environments; violates Gate M1 frozen contract.
* **Option 2 (Full Rollback to Zero-Dependency Mocking):** Implement WebSocket and PostgreSQL wire protocols from scratch.
  - *Deficiency:* High implementation complexity and risk of non-standard protocol bugs; unwarranted diversion from core HFT operating system contracts.
* **Option 3 (Explicit Approval with Zero-Tolerance Exact Pinning):** Authorize `ws` and `pg` as audited runtime dependencies, require exact version strings for all production and development dependencies in `package.json`, and verify exact package versions at test time.

## Decision Outcome

Chosen option: **Option 3**. We authorize `ws@8.19.0` and `pg@8.23.1`, and enforce strict version pinning across all dependencies.

### Authorized Runtime Dependencies

| Package Name | Exact Version Pin | Purpose / Operational Boundary | Verification / Conformance Test |
| :--- | :--- | :--- | :--- |
| `json-canonicalize` | `3.0.1` | RFC 8785 Canonical JSON serialization | `suite01_serialization.test.ts` (`JCS-PACKAGE-INTEGRITY-024`) |
| `ws` | `8.19.0` | In-process & loopback market data and order feed transport | `suite14_websocket_portfolio.test.ts` |
| `pg` | `8.23.1` | PostgreSQL 16.8 ACID transactional persistence and row locking | `suite17_real_postgres_integration.test.ts` |

### Authorized Development Dependencies

| Package Name | Exact Version Pin | Purpose |
| :--- | :--- | :--- |
| `@types/node` | `20.12.7` | Node.js standard library type definitions |
| `@types/pg` | `8.23.1` | PostgreSQL client type definitions |
| `@types/ws` | `8.18.2` | WebSocket type definitions |
| `tsx` | `4.23.15` | TypeScript execution runner for test workers |
| `typescript` | `5.4.5` | TypeScript compiler (`tsc --noEmit`) |
| `vitest` | `1.6.0` | Unit and acceptance test framework |

### Invariants and Policy Rules

1. **No Semver Range Operators:** `package.json` must contain zero `^`, `~`, `>`, or `<` characters in both `dependencies` and `devDependencies`.
2. **Loopback Only for Simulated WebSocket:** The `ws` library must be bound exclusively to `127.0.0.1` / localhost in simulation test suites; external network socket listening is prohibited.
3. **Database URL Environment Configuration:** The `pg` client connects only to the connection string provided in `DATABASE_URL`. In environments where `DATABASE_URL` is omitted, native PostgreSQL integration suites skip cleanly rather than failing ungracefully.

## Traceability

- **Specification Reference:** Gate M1 Spec §1.3, §6.1 (`AUDIT-45`).
- **Configuration File:** `Market-HFT-OS/package.json`.
- **Integrity Test:** `JCS-PACKAGE-INTEGRITY-024` in `tests/acceptance/suite01_serialization.test.ts`.
