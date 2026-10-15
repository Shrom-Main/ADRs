# POC-001 — Gate Authorization & Governance Sign-Off Ledger

| Attribute | Project Record |
| :--- | :--- |
| **Project Identifier** | `POC-001` (Market HFT OS) |
| **Controlling Authority** | Project Owner & Independent Audit Desk |
| **Companion Repositories** | `Shrom-Main/Market-HFT-OS` & `Shrom-Main/ADRs` |
| **Operating Boundary** | Strict DRY_RUN / Paper Simulation; Actuals Execution strictly disabled |

---

## 1. Gate Authorization History

| Milestone Gate | Sign-Off Date (UTC) | Authorizing Authority | Authorized Commit Baseline | Conformance Deliverables & Verified Scope | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Gate M0** | 2026-10-10 | Project Owner | `Market-HFT-OS: 582637b` | Project Charter v0.2.4; strict quarantine isolation of `_salvage/`; zero-credential environment; root Git initialization. | **APPROVED** |
| **Gate M1** | 2026-10-11 | Project Owner | `ADRs: 77eff71`<br>`Market-HFT-OS: 70121a0` | Frozen Normative Design Specification v1.13; 4-claim promotion state machine; JCS canonicalization; subunit arithmetic. | **APPROVED** |
| **Gate M2** | 2026-10-11 | Project Owner | `Market-HFT-OS: cbafb60`<br>`ADRs: commit cbafb60 companion` | Execution engine; loopback WebSocket transport; simulated gateway; dual-ledger safety isolation; 15 suites (106 tests). | **APPROVED** |
| **Gate M3** | 2026-10-15 | Project Owner & Audit Desk | `Market-HFT-OS: 0ee073e` (Tag: `POC-001-Gate-M3-Verified`)<br>`ADRs: 3daed52` (Tag: `POC-001-Gate-M3-Verified`) | Durable file-backed recovery journal; separate-process crash recovery; native PostgreSQL 16.8 concurrency & commit reconciliation; ActualsGuard dual-ledger verification; Decision OD-02 codification (19 suites, 158 passed). | **APPROVED / CLOSED** |
| **Post-M3 Security Maintenance** | 2026-10-15 | Project Owner (`Decision OD-03`) | `Market-HFT-OS: 80c4bfd`<br>`ADRs: current` | Dependency security upgrade (`ws@8.22.0`, `vitest@4.1.12`, `vite@6.4.4`, `esbuild@0.25.0`) achieving `0 vulnerabilities` in `npm audit` while strictly preserving exact version pinning and the 158-test baseline. | **MAINTENANCE CLOSED** |

---

## 2. Gate Decision Notes & Operating Boundaries

1. **Gate M0 (Quarantine & Environment Isolation)**:
   - Approved operating under strict read-only salvage inspection.
   - Live broker/exchange APIs prohibited; mock and loopback transports only.

2. **Gate M1 (Design Readiness Specification Freeze)**:
   - Specification frozen as authoritative normative contract.
   - Embedded errata addressed under versioned addendum / Erratum v1.14 (unifying gateway digest binding to full `ClaimSigningPayload` SHA-256 and fail-closed key validation).

3. **Gate M2 (Simulated Execution & Dual-Ledger Isolation)**:
   - Paper execution pipeline operational with monotonic virtual clocks.
   - `ActualsGuard` enforced fail-closed (`E-ERR-020` and `E-ERR-025`).

4. **Gate M3 (Persistence, Crash Recovery & Native PostgreSQL Concurrency)**:
   - Separate-process crash worker restarts validated against WAL and snapshot storage.
   - Real PostgreSQL 16.8 server verification completed on `localhost:5432` with zero skips across all 6 test cases in Suite 17.
   - WAL boundary normalization, fail-closed torn-tail truncation, and single-pass fill recovery integrated and verified.

5. **Project Owner Decision OD-02 (Hybrid Scope Resolution for Frozen Spec §8.2)**:
   - `PROP-INV-001` (7-bucket warehouse inventory transitions), `META-FEE-001` (Amazon closing fee monotonicity), and `HIST-REPLAY-001` (AIStudio March 2026 SS304 clamp landed cost fixture at ₹38.21) are legacy upstream retail/e-commerce artifacts from the AIStudio template and are formally waived / de-scoped from the Market-HFT-OS runtime baseline.
   - `FUZZ-CLOCK-001` (+600s clock skew -> `E-ERR-007: CLOCK_SKEW_EXCEEDED`) is retained, implemented, and verified in `suite13_market_feed_execution.test.ts`, expanding the verified baseline to 158 passed tests across 19 suites (0 skipped, 0 failed).
   - Gate M3 status is authoritatively confirmed as **APPROVED / CLOSED**.

6. **Project Owner Decision OD-03 (Post-M3 Dependency Security Upgrade)**:
   - Upgraded `ws` to exact `"8.22.0"` and `vitest` to exact `"4.1.12"` (with pinned overrides for `vite@6.4.4` and `esbuild@0.25.0`), eliminating all advisories (`GHSA-58qx-3vcg-4xpx`, `GHSA-96hv-2xvq-fx4p`, `GHSA-5gmw-xhrv-c9v3`, `GHSA-85c8-ppgw-ccpr`, `GHSA-67mh-4wv8-2f99`, `GHSA-5xrq-8626-4rwp`) and achieving `found 0 vulnerabilities` in `npm audit`.
   - The verified Gate M3 closure baseline was permanently anchored with annotated Git tag `POC-001-Gate-M3-Verified` at commit `0ee073e` in `Market-HFT-OS` and commit `3daed52` in `ADRs`.
   - The post-M3 security maintenance commit advances `Market-HFT-OS` to `80c4bfd` while strictly maintaining the 158-test baseline (19 suites passed, 0 skipped, 0 failed) and zero-caret pinning policy (`ADR-0004`).
