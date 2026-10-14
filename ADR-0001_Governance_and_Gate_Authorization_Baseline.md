# ADR-0001: Governance and Gate Authorization Baseline

* **Status:** Accepted
* **Date:** 2026-10-14
* **Deciders:** Project Owner, System Architect, Independent Audit Desk
* **Technical Domain:** Project Governance, Lifecycle Gates, Authorization Hierarchy

---

## Context and Problem Statement

`PROJECT_CHARTER.md` v0.2.4 was drafted at commit `582637b` establishing a strict `PROPOSED — awaiting project-owner approval` state and a `Strict Read-Only prior to Gate M0 authorization` operating rule (§10.1). As the project progressed across Gates M1, M2, and M3 (advancing from baseline `582637b` to `abfaa04`, `70121a0`, `cbafb60`, `7415c61`, and `a1bd359`), implementation proceeded based on interactive owner authorizations and audit verifications, but the in-tree charter header was not retroactively mutated in Git.

This created an authority ambiguity (`F-03`): a literal reading of `PROJECT_CHARTER.md` v0.2.4 would classify all subsequent implementation commits as unauthorized, even though Gate M1 design freeze (`77eff71`), Gate M1 conformance matrix (`70121a0`), Gate M2 integration (`cbafb60`), and Gate M3 persistence (`a1bd359`) were formally authorized and documented in gate conformance reports.

## Decision Drivers

1. Maintain historical immutability of `PROJECT_CHARTER.md` v0.2.4 at baseline commit `582637b`.
2. Establish an authoritative, versioned gate authorization ledger documenting the retroactive and forward approvals of Gates M0, M1, M2, and M3.
3. Formally delineate the operational boundary: strict `DRY_RUN` / paper simulation isolation with actuals ledger execution permanently blocked.
4. Harmonize the documentary authority hierarchy between `Shrom-Main/ADRs` and `Shrom-Main/Market-HFT-OS`.

## Considered Options

* **Option 1:** Retroactively edit `PROJECT_CHARTER.md` in `Market-HFT-OS` and change the header from `PROPOSED` to `APPROVED`.
* **Option 2:** Adopt this Architecture Decision Record (`ADR-0001`) alongside `GATE_AUTHORIZATION_LEDGER.md` in `ADRs`, establishing the formal gate lineage without mutating the historical charter text at `582637b`.

## Decision Outcome

Chosen option: **Option 2**. We preserve `PROJECT_CHARTER.md` v0.2.4 as the historical foundation and record explicit gate authorizations through this ADR and `GATE_AUTHORIZATION_LEDGER.md`.

### Gate Authorization Lineage

1. **Gate M0 (Quarantine & Environment Isolation):**
   - **Baseline:** `Market-HFT-OS` @ `582637b`.
   - **Approved Scope:** Acceptance of Charter v0.2.4; strict quarantine isolation of legacy `_salvage/`; zero-credential environment; root Git initialization.
2. **Gate M1 (Design Readiness Specification Freeze):**
   - **Baseline:** `ADRs` @ `77eff71` / `Market-HFT-OS` @ `70121a0`.
   - **Approved Scope:** Frozen Normative Design Specification v1.13; 4-claim promotion state machine; JCS canonicalization (RFC 8785); integer subunit money; AUDIT-01 through AUDIT-52 compliance.
3. **Gate M2 (Simulated Execution & Dual-Ledger Isolation):**
   - **Baseline:** `Market-HFT-OS` @ `cbafb60`.
   - **Approved Scope:** Paper execution pipeline; monotonic virtual clock; simulated gateway; loopback WebSocket feed; dual-ledger safety isolation (15 suites, 106 tests).
4. **Gate M3 (Persistence, Crash Recovery & Native PostgreSQL Concurrency):**
   - **Baseline:** `Market-HFT-OS` @ `a1bd359` / `ADRs` @ `c52f668`.
   - **Approved Scope:** File-backed recovery journal; separate-process crash worker recovery; native PostgreSQL 16.8 concurrency & commit reconciliation (19 suites, 153 tests).

### Safety Invariants

- **Zero Real Capital / Simulation Isolation:** No live exchange, broker, bank, or payment gateway API connections are permitted. All order routing is confined to `SimulatedExecutionGateway`.
- **Dual-Ledger Enforcement:** Writes to actuals ledger from simulation contexts are blocked fail-closed with error `E-ERR-020` / `E-ERR-040`. Writes to simulation ledger from actuals contexts are blocked with `E-ERR-025`.
- **Authority Scope:** Decisions affecting design specifications, gate progression, or system contracts require formal ADR entry and Owner concurrence.

## Traceability

- Charter: `Market-HFT-OS/PROJECT_CHARTER.md` (§10.1, §10.2).
- Ledger: `ADRs/GATE_AUTHORIZATION_LEDGER.md`.
- Conformance Reports:
  - `POC-001_Gate_M1_Comprehensive_Conformance_Matrix_Report.md`
  - `POC-001_Gate_M2_Execution_and_Integration_Conformance_Report.md`
  - `POC-001_Gate_M3_Persistence_and_Crash_Recovery_Conformance_Report.md`
