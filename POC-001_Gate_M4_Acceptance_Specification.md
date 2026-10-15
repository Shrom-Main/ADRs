# POC-001 — Gate M4 Acceptance Specification: Bounded End-to-End Research & Capital-Allocation Simulation Gate

| Document Attribute | Specification Record |
| :--- | :--- |
| **Document Identifier** | `POC-001_Gate_M4_Acceptance_Specification` |
| **Milestone Gate** | **Gate M4** — End-to-End Research & Capital-Allocation Acceptance Gate |
| **Document Status** | `FROZEN / AUTHORIZED (OD-05)` |
| **Normative Predecessor** | `POC-001_Gate_M1_Design_Readiness_Specification.md` (v1.13 Final / Erratum v1.14) |
| **Authorizing Authority** | Project Owner Decision `OD-05` (15 October 2026) |
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
  Evidence Ingestion & Provenance Attestation (Envelope: source_id, timestamp, ttl, is_verified)
                                           │
                                           ▼
  Financial & Tax Arithmetic Engine (Rational Subunits, Landed Cost, GST/TCS/TDS Cash Timing)
                                           │
                                           ▼
  Inventory Conservation & Asymmetric Return Drag (7-Bucket Fuzzing, Forward+Reverse Logistics)
                                           │
                                           ▼
  Capital Allocation Decision Gate (Cash-Conversion Cycle, Risk-Free + Risk Hurdle, Downside Buffer)
                                           │
                  ┌────────────────────────┴────────────────────────┐
                  ▼                                                 ▼
       [ALLOCATE_CAPITAL]                                  [DO_NOT_ALLOCATE_CAPITAL]
     (Viable Paper Execution)                           (Quarantine / Edge Decay Reject)
```

---

## 2. Six Core Assessment Priorities & Required Invariants

Gate M4 implementation and acceptance testing must rigorously satisfy the six strategic priorities established in the Project Owner's Bird's-Eye Project Assessment and Decision `OD-05`:

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

### Priority 3: Input Evidence & Provenance Tracking (Envelope & TTL Enforcement)
- Every material input (supplier quote, freight tariff, packaging cost, marketplace listing, fee schedule, tax rate, demand velocity estimate) must carry an explicit cryptographic provenance envelope:
  - `source_id`: Canonical identifier of data origin (e.g., `supp:in:mumbai:metalcraft-ltd`, `mkt:amzn:in:fee-schedule:2026`).
  - `observed_at_utc`: Exact ISO 8601 UTC timestamp of observation.
  - `ttl_seconds`: Time-to-live validity window ($\le 604800\text{s}$ [7 days] for supplier quotes, $\le 86400\text{s}$ [24 hours] for marketplace prices).
  - `is_verified`: Boolean attestation status confirming cryptographic signature verification against `TrustAnchorRegistry`.
- **Fail-Closed Staleness & Provenance Gate**:
  - If any input lacks verification, has an expired TTL, or is missing entirely, the engine **MUST** reject fail-closed and emit `DO_NOT_ALLOCATE_CAPITAL` with explicit machine-readable error codes (`E-M4-UNVERIFIED-INPUT` or `E-M4-STALE-EVIDENCE`).
  - Silent fallbacks, default values, or hallucinated assumptions are strictly prohibited.

### Priority 4: End-to-End Financial & Tax Correctness (Cash-Conversion Cycle & Tax Drag)
- All calculations must use integer subunits (scale 4, 1 subunit = ₹0.0001) or exact rational fractions. Floating-point arithmetic (`number` multiplication/division) is strictly prohibited in financial paths.
- **Comprehensive Cost Stack & Cash-Flow Timing**:
  1. *Purchase Outlay*: Gross supplier price less verified trade discounts (Day 0 cash outflow).
  2. *Inbound Logistics*: Volumetric vs actual weight freight tariff calculation per KAT-03.
  3. *Packaging & Kitting*: Barcoding, polybagging, and labeling costs.
  4. *Marketplace Fees*: Exact category referral fees, closing fees per fee schedule, weight handling fees, and FBA storage fees.
  5. *Working-Capital Tax Drag & Holdback Modeling*:
     - Upfront 18% GST paid on procurement and logistics ties up cash until offset against output tax liability.
     - Section 52 CGST Act: Marketplace Tax Collected at Source (TCS) of 1.00% withheld on gross sales.
     - Section 194-O Income Tax Act: Tax Deducted at Source (TDS) of 1.00% withheld on marketplace disbursements.
     - These tax holdbacks directly extend working-capital lock-up and must not be treated as immediate cash inflows.
  6. *Cash-Conversion Cycle (CCC)*:
     $$\text{CCC Days} = \text{Procurement Lead Time Days} + \text{Warehouse Dwell Days} + \text{Marketplace Settlement Delay Days}$$
     Capital lock-up duration is modeled over full CCC (e.g. $7 + 14 + 14 = 35\text{ days}$).
  7. *Asymmetric Return & Damaged-Inventory Drag*:
     - On marketplace returns, forward fulfillment fees and reverse logistics fees are unrecoverable.
     - Customer returns entering `CUSTOMER_RETURNED_PENDING_INSPECTION` transition to `DAMAGED_QUARANTINED` at an empirical attrition rate (e.g. 2% to 16%), destroying cost basis while consuming logistics fees.
     - `PROP-INV-001` 7-bucket inventory conservation holds strictly at every transition.

### Priority 5: Decision Quality & Opportunity Cost Hurdle Gating
- The capital allocation engine must evaluate opportunities against strict hurdle thresholds:
  - **Risk-Adjusted Opportunity Cost Hurdle**:
    $$\text{Hurdle Rate} = \text{Sovereign 91-Day T-Bill Yield (6.50\%)} + \text{Illiquidity / Execution Risk Premium (8.50\%)} = 15.00\% \text{ annualized}$$
  - **Annualized Return on Locked Working Capital (RoWC)**:
    $$\text{Annualized RoWC} = \frac{\text{Net After-Tax Contribution}}{\text{Peak Working Capital Outlay}} \times \frac{365}{\text{CCC Days}}$$
    Must strictly exceed the Hurdle Rate ($\text{Annualized RoWC} \ge 15.00\%$).
  - **Minimum Cash-on-Cash Margin**: $\ge 20.00\%$ net after all fees, taxes, and return provisions.
  - **Maximum CCC Duration**: $\le 45\text{ days}$.
  - **Downside Breakeven Buffer**: Must withstand a $\ge 15.00\%$ drop in marketplace selling price without negative contribution.
- **Fail-Closed Negative Decision Rule**: If any hurdle is breached, evidence provenance is defective, or liquidity is inadequate, the engine **MUST** deterministically emit `DO_NOT_ALLOCATE_CAPITAL` with a machine-readable list of failing constraints (`E-M4-HURDLE-BREACHED`, `E-M4-MARGIN-BELOW-HURDLE`, `E-M4-RETURN-DRAG-EXCEEDED`, etc.).

### Priority 6: Repeatability & Edge-Decay Detection
- The system must detect deterioration in unit economics over time:
  - Monotonic fee creep (e.g. Amazon fee schedule revisions).
  - Supplier price increases or lead-time expansion.
  - Competitive price erosion on target marketplace listings.
  - Elevated customer return rates degrading net recovery.
- Re-running the simulation pipeline against degraded parameters must deterministically transition the decision from `ALLOCATE_CAPITAL` to `DO_NOT_ALLOCATE_CAPITAL` and emit a structured audit trail detailing the exact constraint breach.

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

This document is formally **`FROZEN / AUTHORIZED (OD-05)`** by Project Owner Decision `OD-05` (15 October 2026). Implementation of Gate M4 feature code and the accompanying test suite (`suite20_m4_ss304_vertical_slice.test.ts`) is authorized under strict adherence to all out-of-scope boundaries and five core financial invariants.
