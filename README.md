# Market HFT OS — Architecture Decision Records & Conformance Reports

Repository index for architecture decision records (ADRs), frozen specifications, gate authorization ledgers, and conformance reports across [`Shrom-Main/ADRs`](https://github.com/Shrom-Main/ADRs) and [`Shrom-Main/Market-HFT-OS`](https://github.com/Shrom-Main/Market-HFT-OS).

---

## 1. Architecture Decision Records (ADRs)

| ADR Identifier | Title | Status | Date | Core Scope |
| :--- | :--- | :--- | :--- | :--- |
| [`ADR-0001`](./ADR-0001_Governance_and_Gate_Authorization_Baseline.md) | Governance and Gate Authorization Baseline | Accepted | 2026-10-14 | Formalizes Gate M0–M3 lifecycle authority and simulation boundaries. |
| [`ADR-0002`](./ADR-0002_Anchored_Cumulative_COGS_and_Long_Only_Inventory.md) | Anchored Cumulative COGS Allocation and Long-Only Inventory Policy | Accepted | 2026-10-14 | $A(s) = \operatorname{divideHalfEven}(C_0 \cdot s, Q_0)$ and `E-ERR-044` short position ban. |
| [`ADR-0003`](./ADR-0003_File_Backed_WAL_Durability_and_Crash_Recovery.md) | File-Backed WAL Durability, Torn-Tail Recovery Policy, and Crash Recovery Contract | Accepted | 2026-10-14 | `FileBackedDurableRecoveryJournal`, CRLF/LF normalization, poisoning, and recovery parity. |
| [`ADR-0004`](./ADR-0004_Runtime_Dependency_Adoption_and_Version_Pinning.md) | Runtime Dependency Adoption and Version Pinning Policy | Accepted | 2026-10-14 | Strict exact version pinning for `json-canonicalize@3.0.1`, `ws@8.19.0`, and `pg@8.23.1`. |

---

## 2. Governance & Gate Authorization

* **Gate Authorization Ledger:** [`GATE_AUTHORIZATION_LEDGER.md`](./GATE_AUTHORIZATION_LEDGER.md) — Authoritative sign-off record for Gates M0, M1, M2, M3, M4, M4.1, M4.2, M4.3, M5, M6, M6.1, and M6.2.

---

## 3. Gate Conformance Reports & Audit Evidence

* **Gate M6.2 Test Execution Results (JSON):** [`POC-001_Gate_M6_2_Test_Execution_Results.json`](./POC-001_Gate_M6_2_Test_Execution_Results.json) — Vitest v4.1.12 machine-readable output (208 passed tests across 24 suites).
* **Gate M6.2 Typecheck Results (UTF-8):** [`POC-001_Gate_M6_2_Typecheck_Execution_Results.txt`](./POC-001_Gate_M6_2_Typecheck_Execution_Results.txt) — TypeScript 5.4.5 typecheck output (0 errors).
* **Gate M6.1 Test Execution Results (JSON):** [`POC-001_Gate_M6_1_Test_Execution_Results.json`](./POC-001_Gate_M6_1_Test_Execution_Results.json) — Vitest v4.1.12 machine-readable output (200 passed tests across 23 suites).
* **Gate M6.1 Typecheck Results (UTF-8):** [`POC-001_Gate_M6_1_Typecheck_Execution_Results.txt`](./POC-001_Gate_M6_1_Typecheck_Execution_Results.txt) — TypeScript 5.4.5 typecheck output (0 errors).
* **Gate M6 Test Execution Results (JSON):** [`POC-001_Gate_M6_Test_Execution_Results.json`](./POC-001_Gate_M6_Test_Execution_Results.json) — Vitest v4.1.12 machine-readable output (192 passed tests across 22 suites).
* **Gate M6 Typecheck Results (UTF-8):** [`POC-001_Gate_M6_Typecheck_Execution_Results.txt`](./POC-001_Gate_M6_Typecheck_Execution_Results.txt) — TypeScript 5.4.5 typecheck output (0 errors).
* **Gate M5 Test Execution Results (JSON):** [`POC-001_Gate_M5_Test_Execution_Results.json`](./POC-001_Gate_M5_Test_Execution_Results.json) — Vitest v4.1.12 machine-readable output (185 passed tests across 21 suites).
* **Gate M5 Typecheck Results (UTF-8):** [`POC-001_Gate_M5_Typecheck_Execution_Results.txt`](./POC-001_Gate_M5_Typecheck_Execution_Results.txt) — TypeScript 5.4.5 typecheck output (0 errors).
* **Gate M4.3 Test Execution Results (JSON):** [`POC-001_Gate_M4_3_Test_Execution_Results.json`](./POC-001_Gate_M4_3_Test_Execution_Results.json) — Vitest v4.1.12 machine-readable output (178 passed tests).
* **Gate M4.3 Typecheck Results (UTF-8):** [`POC-001_Gate_M4_3_Typecheck_Execution_Results.txt`](./POC-001_Gate_M4_3_Typecheck_Execution_Results.txt) — TypeScript 5.4.5 typecheck output (0 errors).
* **Gate M4.2 Test Execution Results (JSON):** [`POC-001_Gate_M4_2_Test_Execution_Results.json`](./POC-001_Gate_M4_2_Test_Execution_Results.json) — Vitest v4.1.12 machine-readable output (175 passed tests).
* **Gate M4.2 Typecheck Results (UTF-8):** [`POC-001_Gate_M4_2_Typecheck_Execution_Results.txt`](./POC-001_Gate_M4_2_Typecheck_Execution_Results.txt) — TypeScript 5.4.5 typecheck output for commit `1f3f876`.
* **Gate M4.1 Test Execution Results (JSON):** [`POC-001_Gate_M4_1_Test_Execution_Results.json`](./POC-001_Gate_M4_1_Test_Execution_Results.json) — Vitest v4.1.12 machine-readable output (172 passed tests).
* **Gate M4.1 Typecheck Results (UTF-8):** [`POC-001_Gate_M4_1_Typecheck_Execution_Results.txt`](./POC-001_Gate_M4_1_Typecheck_Execution_Results.txt) — TypeScript 5.4.5 typecheck output for commit `a1053b0`.
* **Gate M4 Vertical Slice Conformance Report:** [`POC-001_Gate_M4_Vertical_Slice_Conformance_Report.md`](./POC-001_Gate_M4_Vertical_Slice_Conformance_Report.md) (`POC-001-M4-CONF-001`) — 20 test files / 169 tests passed.
* **Gate M4 Test Execution Results (JSON):** [`POC-001_Gate_M4_Test_Execution_Results.json`](./POC-001_Gate_M4_Test_Execution_Results.json) — Vitest v4.1.12 machine-readable output (169 passed tests).
* **Gate M4 Typecheck Results (UTF-8):** [`POC-001_Gate_M4_Typecheck_Execution_Results.txt`](./POC-001_Gate_M4_Typecheck_Execution_Results.txt) — TypeScript 5.4.5 typecheck output for commit `9bc249a`.
* **Pre-M4 Conformance Reconciliation Report:** [`POC-001_Pre_M4_Conformance_Reconciliation_Report.md`](./POC-001_Pre_M4_Conformance_Reconciliation_Report.md) — Predecessor gate reconciliation & full §8.2 verification.
* **Pre-M4 Conformance Test Results (JSON):** [`POC-001_Pre_M4_Conformance_Test_Execution_Results.json`](./POC-001_Pre_M4_Conformance_Test_Execution_Results.json) (161 passed tests).
* **Pre-M4 Typecheck Results (UTF-8):** [`POC-001_Pre_M4_Typecheck_Execution_Results.txt`](./POC-001_Pre_M4_Typecheck_Execution_Results.txt) (commit `cf0faf1`).
* **Gate M3 Conformance Report (v1.4.0 Final):** [`POC-001_Gate_M3_Persistence_and_Crash_Recovery_Conformance_Report.md`](./POC-001_Gate_M3_Persistence_and_Crash_Recovery_Conformance_Report.md) (`POC-001-M3-CONF-001`) — 19 test files / 158 tests passed.
* **Gate M3 WAL Boundary Normalization Addendum:** [`POC-001_Gate_M3_WAL_Boundary_Normalization_Audit_Addendum.md`](./POC-001_Gate_M3_WAL_Boundary_Normalization_Audit_Addendum.md) (`POC-001-M3-ADDENDUM-001`)
* **Gate M3 Test Execution Results (JSON):** [`POC-001_Gate_M3_Test_Execution_Results.json`](./POC-001_Gate_M3_Test_Execution_Results.json) — Tag `POC-001-Gate-M3-Verified` output (158 passed tests).
* **Gate M3 Typecheck Results (UTF-8):** [`POC-001_Gate_M3_Typecheck_Execution_Results.txt`](./POC-001_Gate_M3_Typecheck_Execution_Results.txt) — TypeScript 5.4.5 typecheck output for commit `0ee073e`.
* **Gate M2 Conformance Report:** [`POC-001_Gate_M2_Execution_and_Integration_Conformance_Report.md`](./POC-001_Gate_M2_Execution_and_Integration_Conformance_Report.md) (15 suites / 106 tests).
* **Gate M2 Test Execution Results (JSON):** [`POC-001_Gate_M2_Test_Execution_Results.json`](./POC-001_Gate_M2_Test_Execution_Results.json)
* **Gate M1 Comprehensive Conformance Matrix:** [`POC-001_Gate_M1_Comprehensive_Conformance_Matrix_Report.md`](./POC-001_Gate_M1_Comprehensive_Conformance_Matrix_Report.md) (12 suites / 53 tests; expanded baseline 20 suites / 169 tests).
* **Gate M1 Implementation Report:** [`POC-001_Gate_M1_Implementation_Execution_Report.md`](./POC-001_Gate_M1_Implementation_Execution_Report.md) (11 suites / 43 tests).

---

## 4. Frozen Normative Specifications

* **Gate M6 Multi-Agent and Bitemporal Replay Specification:** [`POC-001_Gate_M6_Multi_Agent_and_Bitemporal_Replay_Specification.md`](./POC-001_Gate_M6_Multi_Agent_and_Bitemporal_Replay_Specification.md) (`FROZEN / AUTHORIZED (OD-10)`).
* **Gate M5 Signal Bus & Group Simulation Specification:** [`POC-001_Gate_M5_Signal_Bus_and_Group_Simulation_Specification.md`](./POC-001_Gate_M5_Signal_Bus_and_Group_Simulation_Specification.md) (`FROZEN / AUTHORIZED (OD-09)`).
* **Gate M5 Portfolio Capital Rationing Specification:** [`POC-001_Gate_M5_Portfolio_Capital_Rationing_Specification.md`](./POC-001_Gate_M5_Portfolio_Capital_Rationing_Specification.md) (`FROZEN / AUTHORIZED (OD-09)`).
* **Gate M4 Acceptance Specification:** [`POC-001_Gate_M4_Acceptance_Specification.md`](./POC-001_Gate_M4_Acceptance_Specification.md) (`FROZEN / AUTHORIZED (OD-05)`).
* **Gate M4 SS304 Vertical Slice Test Scenario:** [`POC-001_Gate_M4_SS304_Vertical_Slice_Test_Scenario.md`](./POC-001_Gate_M4_SS304_Vertical_Slice_Test_Scenario.md) (`FROZEN / AUTHORIZED (OD-05)`).
* **Gate M1 Specification:** [`POC-001_Gate_M1_Design_Readiness_Specification.md`](./POC-001_Gate_M1_Design_Readiness_Specification.md) (v1.13 Final / Erratum v1.14 Normative Contract, blob `ac8899da3a6dcccb2c612247302e6f57fc566472`).
* **Rendered PDF Review Copy:** [`ADRXX3.pdf`](./ADRXX3.pdf) (Subordinate rendered reference snapshot).

---

## 5. Independent Review Notes & Remediation

* **Review Note 003 / 004 (ARGON-REV-POC001-20261015-R3):** [`Review notes/Review_notes003.md`](./Review%20notes/Review_notes003.md)
* **Comprehensive Review Notes Remediation Report:** [`Review notes/ARGON_REVIEW_NOTES_REMEDIATION_REPORT.md`](./Review%20notes/ARGON_REVIEW_NOTES_REMEDIATION_REPORT.md) (`POC-001-REM-001`)
* **Review Note 002 (ARGON-REV-POC001-20261014):** [`Review notes/Review_notes002.md`](./Review%20notes/Review_notes002.md)
* **Review Note 001:** [`Review notes/Review_notes001.md`](./Review%20notes/Review_notes001.md)
* **ADRs Governance Review Note:** [`Review notes/argon_review_note_adrs.md`](./Review%20notes/argon_review_note_adrs.md)
* **Market-HFT-OS Implementation Review Note:** [`Review notes/argon_review_note_market_hft_os.md`](./Review%20notes/argon_review_note_market_hft_os.md)

---

## 6. Pre-Charter Foundational Research Memos (Non-Normative)

The following documents represent pre-charter conceptual discussions and design exploration memos. They are non-normative foundational research materials, cross-referenced in `Market-HFT-OS/RESEARCH_CORPUS_INDEX.md`:

| File | Document Role | Context |
| :--- | :--- | :--- |
| `002.docx` | Pre-Charter Memo | Autonomous discovery loops and feedback mechanisms. |
| `003.docx` | Pre-Charter Memo | Global discovery and India-first commercialization. |
| `004.docx` | Pre-Charter Memo | Investment Thesis as primary portfolio allocation unit. |
| `005.docx` | Pre-Charter Memo | Six-Engine mapping of financial HFT concepts to commodity arbitrage. |
| `006.docx` | Pre-Charter Memo | Development environment split (Antigravity primary vs AI Studio). |
| `007.docx` | Pre-Charter Memo | 7-stage commercial pipeline architecture. |
| `008.docx` | Pre-Charter Memo | Market simulation, tail-risk management, and emergent profitability. |
| `009.docx` | Pre-Charter Memo | Initial read-only codebase audit plan. |

*(Note: `001.docx` resides in foundational project archives as indexed in `RESEARCH_CORPUS_INDEX.md`).*

---

## 7. Synchronization

Both repositories are synchronized with GitHub using the secure synchronization helper scripts in `Market-HFT-OS/scripts/sync_repos.py`.
