# POC-001 — Gate M4 Acceptance Specification: Bounded End-to-End Research & Capital-Allocation Simulation Gate

| Document Attribute | Specification Record |
| :--- | :--- |
| **Document Identifier** | `POC-001_Gate_M4_Acceptance_Specification` |
| **Milestone Gate** | **Gate M4** — End-to-End Research & Capital-Allocation Acceptance Gate |
| **Document Status** | `PROPOSED / FOR OWNER REVIEW` |
| **Normative Predecessor** | `POC-001_Gate_M1_Design_Readiness_Specification.md` (v1.13 Final / Erratum v1.14) |
| **Authorizing Authority** | Project Owner & Independent Audit Desk |
| **Operating Boundary** | Strict Dry-Run Simulation; Paper Trading Only; Zero Real Capital Execution |
| **Focus Vertical Slice** | DIN 3017 W4 Stainless Steel SS304 Worm-Drive Hose Clamp (Pack of 10, 16–25mm) |

---

## 1. Milestone Objective & Scope Definition

Gate M4 transitions Market HFT OS from infrastructure-level persistence and execution testing (Gates M1–M3) into a **bounded, end-to-end commercial research and capital-allocation simulation engine**.

The core objective of Gate M4 is to prove that the operating system can take raw, provenance-backed market and supplier evidence for a physical arbitrage opportunity, evaluate all financial, tax, and inventory constraints with zero precision loss, and deterministically render high-conviction capital allocation recommendations (`ALLOCATE_CAPITAL` vs `DO_NOT_ALLOCATE_CAPITAL`).

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                               GATE M4 PIPELINE ARCHITECTURE                            │
└────────────────────────────────────────────────────────────────────────────────────────┘
  Supplier & Market Data Feeds (Signed Quotes, Marketplace Catalogs, Fee Schedules)
                                           │
                                           ▼
  Evidence Ingestion & Provenance Attestation (Ed25519 Signed Claims, RFC 8785 Canonical)
                                           │
                                           ▼
  Financial & Tax Arithmetic Engine (Rational Subunits, Landed Cost, GST Netting, Amazon Fees)
                                           │
                                           ▼
  Inventory Conservation & Working-Capital Duration (7-Bucket Fuzzing, Outlay Recovery Days)
                                           │
                                           ▼
  Capital Allocation Decision Gate (Hurdle Rate, Downside Margin of Safety, Liquidity Check)
                                           │
                  ┌────────────────────────┴────────────────────────┐
                  ▼                                                 ▼
       [ALLOCATE_CAPITAL]                                  [DO_NOT_ALLOCATE_CAPITAL]
     (Viable Paper Execution)                           (Quarantine / Edge Decay Reject)
```

---

## 2. Six Core Assessment Priorities

Gate M4 implementation and acceptance testing must rigorously satisfy the six strategic priorities established in the Project Owner's Bird's-Eye Project Assessment:

### Priority 1: Predecessor Conformance Closure
- All architectural invariants established in Gates M1 through M3 must be maintained without regression.
- The 161-test baseline (across 19 suites) must continue to pass with 0 skipped and 0 failed against live PostgreSQL 16.8.
- Zero normative waivers remain across Frozen Specification §8.1 and §8.2.

### Priority 2: Complete Research Vertical Slice (SS304 Pack-of-10 Hose Clamp)
- All Gate M4 acceptance criteria must be proven against the canonical physical arbitrage fixture:
  - **Product**: DIN 3017 W4 Stainless Steel SS304 Worm-Drive Hose Clamp (Pack of 10, 16–25mm bandwidth 9mm).
  - **HSN / Tax Category**: `73269099` (Articles of iron or steel, other), 18% GST standard bracket with 100% Input Tax Credit (ITC) eligibility.
  - **Sourcing Baseline**: Verified B2B wholesale invoice / RFQ quote at ₹25.0000 per pack.
  - **Landed Cost Breakdown**: Exactly ₹38.2100 per pack (purchase ₹25.0000, freight ₹4.5000, packaging ₹3.2000, insurance ₹1.0000, inspection & net customs/GST ₹4.5100).
  - **Marketplace Target**: Amazon India FBA listing at ₹105.0000 to ₹110.0000 gross consumer selling price.

### Priority 3: Input Evidence & Provenance Tracking
- Every piece of input data (supplier quotes, freight tariffs, packaging quotes, marketplace listings, fee schedules) must be accompanied by cryptographically verifiable provenance:
  - **Attester Signature**: Valid Ed25519 signature over RFC 8785 canonical JSON claim payload.
  - **Capture Timestamp**: ISO 8601 UTC timestamp bounded within strict freshness windows ($\le 7\text{ days}$ for supplier quotes, $\le 24\text{ hours}$ for marketplace listings).
  - **Attester Identity**: Bound to an unrevoked trust anchor in `TrustAnchorRegistry`.
  - **Fail-Closed Rejection**: Ingestion of unauthenticated, backfilled, or expired claims must immediately reject fail-closed (`E-ERR-001: CLAIM_TYPE_UNAUTHORIZED` or `E-ERR-007: CLOCK_SKEW_EXCEEDED`).

### Priority 4: End-to-End Financial & Tax Correctness
- All calculations must use integer subunits (scale 4, 1 subunit = ₹0.0001) or exact rational fractions. Floating-point arithmetic (`number` multiplication/division) is strictly prohibited in financial paths.
- **Comprehensive Cost Stack**:
  1. *Purchase Outlay*: Gross supplier price less verified trade discounts.
  2. *Inbound Logistics*: Volumetric vs actual weight freight tariff calculation per KAT-03.
  3. *Packaging & Kitting*: Barcoding, polybagging, and labeling costs.
  4. *Marketplace Fees*: Exact category referral fees, closing fees per fee schedule, weight handling fees, and FBA storage fees.
  5. *Tax Engine*: Forward GST calculation on marketplace sales, offset by verified Input Tax Credit (ITC) on procurement and logistics; income tax reserve provisions.
  6. *Working-Capital Lock-Up*: Outlay recovery duration ($k_{\text{rec}} - k_{\text{outlay}}$) computed per `REC-OUTLAY-001` to determine annualized capital turnover velocity.
  7. *Inventory Drag*: Expected write-offs for customer returns and transit damage factored into net unit economics.

### Priority 5: Decision Quality & Negative Hurdle Gating
- The capital allocation engine must evaluate opportunities against strict hurdle thresholds:
  - **Minimum Return on Peak Funding (RoPF)**: $\ge 25.00\%$ annualized.
  - **Minimum Cash-on-Cash Margin**: $\ge 20.00\%$ net after all fees, taxes, and return provisions.
  - **Maximum Outlay Recovery Window**: $\le 45\text{ days}$.
  - **Downside Breakeven Buffer**: Must withstand a $\ge 15.00\%$ drop in marketplace selling price without negative contribution.
- **Fail-Closed Negative Decision Rule**: If any hurdle is breached, evidence provenance is defective, or liquidity is inadequate, the engine **MUST** deterministically emit `DO_NOT_ALLOCATE_CAPITAL` with a machine-readable list of failing constraints. Silent coercion or optimistic approval is strictly prohibited.

### Priority 6: Repeatability & Edge-Decay Detection
- The system must detect deterioration in unit economics over time:
  - Monotonic fee creep (e.g. Amazon fee schedule revisions).
  - Supplier price increases or lead-time expansion.
  - Competitive price erosion on target marketplace listings.
  - Elevated customer return rates degrading net recovery.
- Re-running the simulation pipeline against degraded parameters must deterministically transition the decision from `ALLOCATE_CAPITAL` to `DO_NOT_ALLOCATE_CAPITAL`.

---

## 3. Strict Out-of-Scope Boundaries for Gate M4

To maintain architectural focus, safety, and strict alignment with the Project Charter, the following capabilities are **EXPLICITLY OUT OF SCOPE** for Gate M4:

```
┌────────────────────────────────────────────────────────────────────────┐
│                     GATE M4 OUT-OF-SCOPE BOUNDARIES                    │
├────────────────────────────────┬───────────────────────────────────────┤
│ BOUNDARY                       │ ENFORCEMENT MECHANISM                 │
├────────────────────────────────┼───────────────────────────────────────┤
│ 1. Real-Money Capital Routing  │ Hard blocked by ActualsGuard          │
│ 2. Autonomous Agent Capital    │ Policy tickets require owner Ed25519  │
│ 3. LLMs in Financial Math      │ Pure TypeScript integer BigInt subunit│
│ 4. Cloud Orchestration Sprawl  │ Self-contained local runtime          │
│ 5. Multi-Strategy Expansion    │ Strictly limited to SS304 clamp slice │
└────────────────────────────────┴───────────────────────────────────────┘
```

1. **No Real-Money Capital Routing or Live Exchange/Broker Connections**:
   - Zero live banking, broker, or payment gateway APIs.
   - All order routing is strictly confined to `SimulatedExecutionGateway`.
   - Dual-ledger `ActualsGuard` remains active fail-closed with `E-ERR-020` / `E-ERR-025`.
2. **No Autonomous Agent Authority to Commit Capital or Promote Evidence**:
   - AI models and subagents cannot authorize capital allocation or promote evidence to production actuals.
   - All capital allocation recommendations require explicit human review or cryptographically signed policy tickets.
3. **No Large Language Models (LLMs) Inside Deterministic Financial Math**:
   - LLMs may assist in unstructured invoice parsing or discovery extraction, but **NEVER** in valuation, pricing, fee calculation, margin analysis, or allocation logic.
   - All financial math is executed exclusively by deterministic TypeScript rational arithmetic.
4. **No Cloud or Orchestration Sprawl**:
   - No Kubernetes, multi-region cloud clusters, or distributed messaging brokers.
   - Gate M4 is verified entirely within the deterministic local runtime with PostgreSQL 16.8 and local loopback WebSocket networking.
5. **No Multi-Strategy Expansion Prior to Single-Slice Validation**:
   - Strategy development is strictly confined to the DIN 3017 SS304 hose-clamp arbitrage vertical slice.
   - No multi-asset, multi-marketplace, or cross-border expansion until the single-slice pipeline is accepted by the Project Owner.

---

## 4. Gate M4 Auditable Acceptance Criteria

| Criteria ID | Acceptance Requirement | Verification Method | Pass Standard |
| :--- | :--- | :--- | :--- |
| **M4-PREC-001** | Zero regressions across Gate M1–M3 baseline | Automated test runner | 161 passed tests across 19 suites (0 skipped, 0 failed) |
| **M4-SLICE-002** | Full execution of SS304 vertical slice pipeline | Integration scenario runner | Ingestion -> Valuation -> Taxes -> 7-Bucket -> Allocation recommendation |
| **M4-MATH-003** | Exact integer subunit calculation of landed cost | Bitwise comparison | Landed cost matches ₹38.2100 (`382100n` subunits) exact |
| **M4-TAX-004** | GST forward calculation & ITC netting accuracy | Financial test assertion | ITC strictly netted against output GST liability |
| **M4-FEE-005** | Amazon marketplace fee schedule evaluation | Monotonic stepping test | Referral + closing + FBA fees calculated with zero drift |
| **M4-DEC-006** | Deterministic allocation on viable opportunity | Scenario A execution | Emits `ALLOCATE_CAPITAL (PAPER_SIMULATION)` with risk bounds |
| **M4-REJ-007** | Deterministic rejection on economic deterioration | Scenario B execution | Emits `DO_NOT_ALLOCATE_CAPITAL` with machine-readable causes |
| **M4-AUTH-008** | Fail-closed quarantine on invalid/missing evidence | Scenario C execution | Rejects unauthenticated/stale claims with zero silent coercion |
| **M4-LOCK-009** | Outlay recovery duration and peak funding bounds | Cash flow engine check | Outlay recovery $\le 45\text{ days}$; Peak funding correctly bounded |
| **M4-INVAR-010** | Dual-ledger safety isolation intact | ActualsGuard security test | Zero writes to actuals ledger without signed owner ticket |

---

## 5. Specification Governance Status

This document is submitted as **`PROPOSED / FOR OWNER REVIEW`**. Implementation of Gate M4 feature code shall commence only upon formal ratification of this specification and the accompanying test scenario document by the Project Owner.
