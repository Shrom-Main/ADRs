# POC-001 — Gate M5 Portfolio Capital Rationing Specification: Multi-Opportunity Working-Capital Allocation, Formula RAG Bridge & Shadow Sandbox

| Document Attribute | Specification Record |
| :--- | :--- |
| **Document Identifier** | `POC-001_Gate_M5_Portfolio_Capital_Rationing_Specification` |
| **Milestone Gate** | **Gate M5** — Multi-Opportunity Portfolio Capital Rationing & Sandbox Formula Stress-Testing |
| **Document Status** | `FROZEN / AUTHORIZED (OD-09)` |
| **Normative Predecessors** | `POC-001_Gate_M1_Design_Readiness_Specification.md`, `POC-001_Gate_M4_Acceptance_Specification.md`, Decisions `OD-05` through `OD-08` |
| **Authorizing Authority** | Project Owner Decision `OD-09` (16 October 2026) |
| **Operating Boundary** | Strict Dry-Run Simulation; Multi-Candidate Portfolio Allocation; Paper Trading Only; Zero Real Capital Execution |
| **Primary Reference Pool** | 4-Candidate Industrial Procurement Pool (SS304 Clamp, SS316 Marine Clamp, Carbon Clamp, Brass Barb) |

---

## 1. Milestone Objective & Scope Definition

Gate M5 elevates Market HFT OS from single-opportunity vertical slice evaluation (Gate M4 / M4.1 / M4.3) to a **multi-opportunity portfolio capital rationing and sandbox formula stress-testing engine**.

In real-world physical and B2B-to-consumer industrial arbitrage, capital is scarce. Multiple potential procurement opportunities compete simultaneously for a finite corporate treasury budget. Gate M5 implements the mathematical and governance mechanisms required to:
1. Ingest an arbitrary pool of $N$ competing arbitrage candidates.
2. Filter each candidate through cryptographic provenance verification and normative unit economics.
3. Rank viable candidates by Risk-Adjusted Annualized Return on Working Capital (RoWC) net of hurdle rate.
4. Ration finite treasury capital across candidates under hard concentration caps and discrete Minimum Order Quantity (MOQ) lot-size constraints.
5. Sweep any unallocated residual cash into a risk-free sovereign 91-day T-Bill reserve, enforcing exact budget conservation ($\sum \text{allocated} + \text{residual} \equiv \text{treasury\_budget}$).
6. Provide a direct bridge to the Governed Formula Registry (`src/research/formulaRegistry.ts`) to execute dual-pass evaluation:
   - **Authoritative Pass**: Bound strictly to `PROMOTED_NORMATIVE` formulas.
   - **Shadow What-If Pass**: Incorporates active `CANDIDATE_UI_MODEL` formulas (e.g., warehouse inventory shrinkage or customs anti-dumping duty) to produce an isolated `ShadowDeltaReport` quantifying rank and decision flips without mutating the authoritative decision.

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                        GATE M5 MULTI-OPPORTUNITY CAPITAL ALLOCATOR                     │
└────────────────────────────────────────────────────────────────────────────────────────┘
  Candidate Opportunity Pool (SS304, SS316 Marine, Carbon Steel, Brass Barb)
                                            │
                                            ▼
  Provenance & TTL Verification Gate (Envelope Verification; Stale/Unverified -> Quarantine)
                                            │
                                            ▼
  Normative Unit Economics Evaluator (FormulaRegistry: PROMOTED_NORMATIVE Formulas)
  (Landed Cost, Net Contribution, Cash Conversion Cycle, Annualized RoWC, Hurdle Drag)
                                            │
                                            ▼
  Competitive Ranking & Priority Queue (Sorted by Excess RoWC = RoWC - Hurdle Rate)
                                            │
                                            ▼
  Discrete Capital Rationing & Sizing Engine:
    ├── Hard Treasury Budget Cap (e.g., ₹50,000.0000 / 500,000,000 subunits)
    ├── Single-Candidate Concentration Cap (e.g., max 50.00% / 5000 bps)
    ├── Discrete MOQ Lot-Sizing (Integer batch step: k * MOQ, no fractional batches)
    └── Sovereign 91-Day T-Bill Sweep (Residual unallocated cash parked at risk-free rate)
                                            │
                                            ├──────────────────────────────────────────┐
                                            ▼                                          ▼
                               [AUTHORITATIVE DECISION]                   [SHADOW SANDBOX PASS]
                                 (PROMOTED_NORMATIVE)                     (CANDIDATE_UI_MODEL)
                                            │                                          │
                                            ▼                                          ▼
                               Deterministic RFC 8785 JCS                   Shadow Delta Report
                                 Canonical Portfolio Record                 (Drag bps, Rank Flips,
                                (SHA-256 Digest Attestation)               Decision Flip Detection)
```

---

## 2. Mathematical Formulations & Rationing Invariants

All calculations are executed in pure `BigInt` rational arithmetic with integer subunits (scale 4, 1 subunit = ₹0.0001) or exact rational fractions (`{ num: bigint, den: bigint }`). Floating-point arithmetic (`number` multiplication/division) is strictly prohibited.

### 2.1. Candidate Unit Economics & RoWC Formulation
For each candidate $i \in \{1, \dots, N\}$:
1. **Landed Cost per Unit ($\text{LC}_i$)**:
   $$\text{LC}_i = \text{purchase\_cost}_i + \text{freight}_i + \text{packaging}_i + \text{insurance}_i + \text{inspection\_customs\_net\_gst}_i$$
2. **Gross Selling Price ($\text{SP}_i$)**: Observed marketplace listing price.
3. **Net Realized Margin / Unit Contribution ($\text{NC}_i$)**:
   $$\text{NC}_i = \text{SP}_i - \text{market\_fees\_net}_i - \text{return\_logistics\_drag}_i - \text{tax\_drag}_i - \text{LC}_i$$
4. **Cash Conversion Cycle ($\text{CCC}_i$)**:
   $$\text{CCC}_i = \text{procurement\_days}_i + \text{inbound\_transit\_days}_i + \text{warehouse\_dwell\_days}_i + \text{marketplace\_settlement\_days}_i$$
5. **Annualized Return on Working Capital ($\text{RoWC}_i$) in Basis Points**:
   $$\text{RoWC\_bps}_i = \text{round}\left( \frac{\text{NC}_i}{\text{LC}_i} \times \frac{365}{\text{CCC}_i} \times 10,000 \right)$$
6. **Risk-Adjusted Excess RoWC ($\text{ExcessRoWC}_i$) in Basis Points**:
   $$\text{ExcessRoWC\_bps}_i = \text{RoWC\_bps}_i - \text{hurdle\_rate\_bps}_i$$

Viability threshold: Candidate $i$ is viable if $\text{ExcessRoWC\_bps}_i > 0$ and $\text{NC}_i > 0$ and provenance is valid.

### 2.2. Ranking & Priority Ordering
All viable candidates are sorted in descending order of $\text{ExcessRoWC\_bps}_i$. If two candidates have identical $\text{ExcessRoWC\_bps}_i$, tie-breaking follows:
1. Shorter Cash Conversion Cycle ($\text{CCC}_i$).
2. Higher absolute Unit Contribution ($\text{NC}_i$).
3. Lexicographical ascending order of `product_id`.

### 2.3. Hard Treasury Budget & Concentration Constraints
Let $B$ be `total_treasury_budget_subunits` and $C_{\max}$ be `max_single_candidate_concentration_bps` (e.g., $5000\text{ bps} = 0.50$).
The maximum capital that can be committed to any single candidate is:
$$B_{\text{cap}, i} = \text{floor}\left( \frac{B \times C_{\max}}{10,000} \right)$$

### 2.4. Discrete MOQ Lot Sizing
Procurement must happen in discrete integer multiples of Minimum Order Quantity ($\text{MOQ}_i$).
Let $\text{BatchOutlay}_{i, 1} = \text{MOQ}_i \times \text{LC}_i$.
If $\text{BatchOutlay}_{i, 1} > B_{\text{cap}, i}$ or $\text{BatchOutlay}_{i, 1} > B_{\text{remaining}}$, the candidate cannot be allocated full batch capital and is rejected with reason `E-M5-BUDGET-EXHAUSTED` or `E-M5-CONCENTRATION-CAP-EXCEEDED`.

Otherwise, the allocated lot count $k_i \in \mathbb{N}_{\ge 1}$ is determined greedily:
$$k_i = \min\left( \left\lfloor \frac{B_{\text{cap}, i}}{\text{BatchOutlay}_{i, 1}} \right\rfloor, \left\lfloor \frac{B_{\text{remaining}}}{\text{BatchOutlay}_{i, 1}} \right\rfloor \right)$$
The allocated capital is:
$$A_i = k_i \times \text{BatchOutlay}_{i, 1} = (k_i \times \text{MOQ}_i) \times \text{LC}_i$$
Remaining budget is decremented:
$$B_{\text{remaining}} \leftarrow B_{\text{remaining}} - A_i$$

### 2.5. Sovereign T-Bill Cash Sweep & Exact Conservation
Any remaining unallocated cash after processing all candidates is swept into the sovereign 91-day T-Bill reserve at `risk_free_rate_bps` ($R_f$, e.g. 650 bps = 6.50%):
$$A_{\text{tbill}} = B_{\text{remaining}}$$
**Budget Conservation Invariant**:
$$\sum_{i \in \text{Allocated}} A_i + A_{\text{tbill}} \equiv B$$
Zero over-allocation, zero overdraft, and zero unallocated leakage are guaranteed.

---

## 3. Rejection Taxonomy & Reason Codes

Every candidate that fails to receive an allocation must be explicitly categorized with a normative machine-readable code:
1. `E-M5-UNVERIFIED-PROVENANCE`: Cryptographic signature missing or failed validation against `TrustAnchorRegistry`.
2. `E-M5-STALE-EVIDENCE`: Input data age exceeds allowable TTL ($\le 7\text{ days}$ for quotes, $\le 24\text{ hours}$ for marketplace).
3. `E-M5-NEGATIVE-CONTRIBUTION`: Unit net contribution $\le 0$.
4. `E-M5-SUB-HURDLE-RETURN`: Annualized RoWC fails to clear the required hurdle rate.
5. `E-M5-CONCENTRATION-CAP-EXCEEDED`: Minimum single MOQ batch outlay exceeds the single-opportunity concentration limit ($B_{\text{cap}}$).
6. `E-M5-BUDGET-EXHAUSTED`: Candidate is viable in isolation, but higher-ranked candidates have consumed available treasury capital such that remaining balance cannot fund 1 full MOQ batch.

---

## 4. Formula Registry Bridge & Dual-Pass Shadow Sandbox

The allocator integrates directly with `FormulaRegistry` (`src/research/formulaRegistry.ts`):
1. **Primary Authoritative Pass**:
   - Only formula cards marked `PROMOTED_NORMATIVE` in `FormulaRegistry` are used to compute official unit economics, RoWC, and capital allocation decisions.
   - Outputs the binding `PortfolioAllocationDecision`.
2. **Shadow What-If Pass (Sandbox Stress-Testing)**:
   - When one or more `CANDIDATE_UI_MODEL` formulas (e.g., warehouse inventory shrinkage drag or customs anti-dumping duty) are provided for what-if evaluation, the engine runs an independent shadow pass over the exact same candidate pool.
   - The shadow pass produces a `ShadowDeltaReport` detailing:
     - Delta in unit net contribution ($\Delta \text{NC}_i$ in subunits and bps)
     - Delta in annualized RoWC ($\Delta \text{RoWC\_bps}_i$)
     - Ranking displacement (e.g., Candidate 2 drops from Rank 2 to Rank 3)
     - Decision flip (e.g., `APPROVED` $\rightarrow$ `REJECTED` or scale-down)
   - The shadow pass operates in strict read-only memory isolation: under no circumstances does an unpromoted `CANDIDATE_UI_MODEL` alter the authoritative allocation record.

---

## 5. RFC 8785 Canonical JSON Serialization (JCS)

To ensure immutable auditability and crash replay reproducibility:
- Every `PortfolioAllocationDecision` record must be canonically serialized via `json-canonicalize@3.0.1`.
- A SHA-256 digest (`portfolio_decision_sha256`) is computed over the JCS canonical byte stream.
- Re-serializing an identical decision record across test runs or crash recoveries must produce a 100% bit-for-bit identical SHA-256 hash.

---

## 6. Acceptance Criteria & Suite 21 Mapping

Acceptance test suite `tests/acceptance/suite21_m5_portfolio_capital_rationing.test.ts` must execute against a realistic 4-candidate industrial pool under a `₹50,000.0000` (`500000000n` subunits) budget:

| Candidate ID | Product Symbol / Description | MOQ | Landed Cost | Expected Outcome |
| :--- | :--- | :--- | :--- | :--- |
| **Candidate 1** | `prod:din3017:ss304:pack-10` (SS304 Clamp) | 500 | ₹38.2100 | **APPROVED (Rank #1)**; Allocated 1 MOQ lot (₹19,105.0000). |
| **Candidate 2** | `prod:din3017:ss316:marine-pack-5` (SS316 Marine) | 250 | ₹80.0000 | **APPROVED (Rank #2)**; Allocated 1 MOQ lot (₹20,000.0000). |
| **Candidate 3** | `prod:carbon:galv:clamp-pack-20` (Carbon Steel) | 1,000 | ₹15.0000 | **REJECTED (`E-M5-BUDGET-EXHAUSTED`)**; Viable in isolation, but requires ₹15,000 while remaining budget is only ₹10,895. |
| **Candidate 4** | `prod:brass:barb:10mm` (Brass Hose Barb) | 100 | ₹45.0000 | **QUARANTINED (`E-M5-UNVERIFIED-PROVENANCE`)**; Unverified quote rejected fail-closed. |

Normative test cases:
1. `M5-PORTFOLIO-RATIONING-001`: Proves budget conservation ($\text{committed} + \text{tbill} \equiv \text{total}$), discrete MOQ sizing, and concentration cap enforcement.
2. `M5-OPPORTUNITY-REJECTION-RIGOR-002`: Proves a viable candidate (Candidate 3) is rejected with `E-M5-BUDGET-EXHAUSTED` when higher-ranked opportunities exhaust capital, preventing fractional execution.
3. `M5-SHADOW-SANDBOX-FORMULA-DELTA-003`: Proves `CANDIDATE_UI_MODEL` formulas run in shadow mode, quantifying rank/decision flip deltas without altering authoritative allocations.
4. `M5-PORTFOLIO-JCS-DETERMINISM-004`: Proves bit-for-bit RFC 8785 canonical serialization and SHA-256 reproducibility of the portfolio decision.
