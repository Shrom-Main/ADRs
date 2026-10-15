# POC-001 — Gate M4 Acceptance Test Scenario: DIN 3017 SS304 Hose-Clamp Vertical Slice

| Document Attribute | Specification Record |
| :--- | :--- |
| **Document Identifier** | `POC-001_Gate_M4_SS304_Vertical_Slice_Test_Scenario` |
| **Milestone Gate** | **Gate M4** — End-to-End Research & Capital-Allocation Acceptance Gate |
| **Document Status** | `FROZEN / AUTHORIZED (OD-05)` |
| **Normative Predecessor** | `POC-001_Gate_M1_Design_Readiness_Specification.md` (v1.13 Final / Erratum v1.14) |
| **Authorizing Authority** | Project Owner Decision `OD-05` (15 October 2026) |
| **Target Commodity** | DIN 3017 W4 Stainless Steel SS304 Worm-Drive Hose Clamp (Pack of 10, 16–25mm) |
| **HSN Code** | `73269099` (Articles of Iron or Steel, Other) |
| **Test Matrix** | **Scenario A** (Viable Opportunity), **Scenario B** (Edge Decay), **Scenario C** (Defective Evidence) |

---

## 1. Physical & Commercial Domain Parameters

The DIN 3017 W4 SS304 pack-of-10 worm-drive hose clamp represents the canonical physical arbitrage fixture for Market HFT OS Gate M4:

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│              CANONICAL SS304 PACK-OF-10 CLAMP PHYSICAL FIXTURE                  │
├───────────────────────────────┬─────────────────────────────────────────────────┤
│ Product ID                    │ prod:din3017:ss304:pack-10                      │
│ Specification Standard        │ DIN 3017 / ISO 9001 W4 Stainless Steel 304     │
│ Clamping Diameter Range       │ 16 mm to 25 mm                                  │
│ Bandwidth / Thickness         │ 9.0 mm / 0.6 mm                                 │
│ Pack Configuration            │ 10 units per retail polyethylene pack           │
│ Pack Net Weight / Gross Weight│ 220 grams / 235 grams                           │
│ Pack Physical Dimensions      │ 120 mm (L) × 80 mm (W) × 35 mm (H)              │
│ Volumetric Weight (KAT-03)    │ 68 grams (Actual weight 235g governs freight)   │
│ GST Rate / ITC Netting        │ 18.00% standard rate / 100% ITC offset eligible │
│ Section 52 CGST TCS Holdback  │ 1.00% withheld on marketplace gross sales       │
│ Section 194-O Income Tax TDS  │ 1.00% withheld on marketplace disbursements     │
│ Cash-Conversion Cycle (CCC)   │ 35 days (7d procurement + 14d dwell + 14d settle)│
│ Risk-Adjusted Hurdle Rate     │ 15.00% annualized (6.50% T-Bill + 8.50% risk)  │
└───────────────────────────────┴─────────────────────────────────────────────────┘
```

---

## 2. Scenario A — Viable Arbitrage Opportunity (`ALLOCATE_CAPITAL`)

### 2.1 Input Evidence & Cryptographic Provenance
1. **Supplier Quote Claim (`CLAIM-SUPP-001`)**:
   - `source_id`: `supp:in:mumbai:metalcraft-ltd` (Registered trust anchor).
   - `observed_at_utc`: `2026-10-15T08:00:00Z` (fresh, age 2 hours).
   - `ttl_seconds`: `604800` (7 days).
   - `is_verified`: `true` (valid Ed25519 signature over canonical JCS payload).
   - Wholesale price: ₹25.0000 per pack (`250000n` subunits).
   - MOQ: 500 packs; Payment terms: Net 15 days; Incoterms: EXW Mumbai.
2. **Inbound Logistics & Customs/Inspection Tariff (`CLAIM-LOG-001`)**:
   - `source_id`: `log:in:bluedart-surface` (`is_verified: true`, `ttl_seconds: 604800`).
   - Freight cost: ₹4.5000 per pack (`45000n`).
   - Insurance & handling: ₹1.0000 per pack (`10000n`).
   - Inspection & customs/GST netting fee: ₹4.5100 per pack (`45100n`).
3. **Packaging & Kitting Claim (`CLAIM-PKG-001`)**:
   - `source_id`: `pkg:in:packpro-solutions` (`is_verified: true`, `ttl_seconds: 604800`).
   - Packaging contractor cost: ₹3.2000 per pack (`32000n`).
4. **Marketplace Listing & Fee Schedule Claim (`CLAIM-MKT-001`)**:
   - `source_id`: `mkt:amzn:in:asin:B09XYZ1234` (`is_verified: true`, `ttl_seconds: 86400`).
   - Gross retail selling price: ₹105.0000 per pack (`1050000n`).
   - Referral fee: 15.00% = ₹15.7500 (`157500n`).
   - Closing fee: ₹10.0000 (`100000n`).
   - FBA pick & pack / weight handling: ₹14.0000 (`140000n`).
   - Total marketplace fees: ₹39.7500 (`397500n`).

### 2.2 Financial & Tax Arithmetic Execution
- **Exact Landed Cost**:
  $$\text{Landed Cost} = 25.0000 + 4.5000 + 3.2000 + 1.0000 + 4.5100 = \text{₹}38.2100 \quad (382100n \text{ subunits})$$
- **Marketplace Disbursement After Fees & Statutory Holdbacks**:
  - Gross Revenue: ₹105.0000 (`1050000n`).
  - Total Marketplace Fees: ₹39.7500 (`397500n`).
  - Section 52 TCS (1.00%): ₹1.0500 (`10500n`).
  - Section 194-O TDS (1.00%): ₹1.0500 (`10500n`).
  - Net Cash Disbursement: $105.0000 - 39.7500 - 1.0500 - 1.0500 = \text{₹}63.1500$ (`631500n`).
- **GST Netting & Tax Settlement**:
  - Output GST liability on sale: ₹16.0169 (18% inclusive in ₹105.00).
  - Input Tax Credit (ITC) on procurement & freight: ₹5.8286.
  - Net GST cash liability: ₹10.1883.
  - Refundable TCS/TDS credit offset: ₹2.1000.
  - Net statutory settlement: $10.1883 - 2.1000 = \text{₹}8.0883$.
- **Unit Net Margin (After Tax & All Fees)**:
  $$\text{Net Contribution} = 63.1500 - 38.2100 - 8.0883 = \text{₹}16.8517 \quad (168517n)$$
  $$\text{Cash-on-Cash Return} = \frac{16.8517}{38.2100} = 44.10\% \quad (> 20.00\% \text{ hurdle})$$
- **Working Capital & Hurdle Evaluation**:
  - Cash-Conversion Cycle: 35 days (7d procurement + 14d warehouse dwell + 14d settlement).
  - Annualized Return on Locked Working Capital:
    $$\text{Annualized RoWC} = 44.10\% \times \frac{365}{35} = 459.9\% \quad (> 15.00\% \text{ hurdle})$$
  - Downside price buffer: $22.50\%$ margin of safety before reaching negative unit contribution.

### 2.3 Expected Deterministic Engine Output
```json
{
  "decision": "ALLOCATE_CAPITAL",
  "execution_mode": "PAPER_SIMULATION",
  "product_id": "prod:din3017:ss304:pack-10",
  "allocation_parameters": {
    "recommended_batch_quantity": 500,
    "committed_capital_inr": "19105.0000",
    "expected_net_margin_bps": 4410,
    "cash_conversion_cycle_days": 35,
    "annualized_rowc_bps": 45990,
    "downside_price_buffer_bps": 2250
  },
  "constraint_evaluations": {
    "evidence_provenance_verified": true,
    "landed_cost_exact_match": true,
    "margin_above_hurdle": true,
    "rowc_above_hurdle": true,
    "cash_conversion_cycle_acceptable": true
  }
}
```

---

## 3. Scenario B — Edge Decay / Fee & Return Deterioration (`DO_NOT_ALLOCATE_CAPITAL`)

### 3.1 Deterioration Injection Parameters
1. **Marketplace Fee Schedule Revision**:
   - Amazon closing fee hiked from ₹10.0000 to ₹25.0000 (`250000n`).
   - Weight handling fee increased to ₹18.0000 (`180000n`).
2. **Supplier Price Creep**:
   - Raw material purchase price creeps from ₹25.0000 to ₹34.0000 (`340000n`).
   - Landed cost increases from ₹38.2100 to ₹47.2100 (`472100n`).
3. **Elevated Return Rate Drag & Quarantined Inventory**:
   - Customer return rate spikes to 16.00% (from nominal 2.00%).
   - Items in `CUSTOMER_RETURNED_PENDING_INSPECTION` transition to `DAMAGED_QUARANTINED`.
   - Forward fulfillment (₹18.00) + reverse logistics fee (₹14.00) are fully absorbed on returns with zero salvage recovery.
   - Amortized return and inventory attrition drag: ₹12.5000 per unit.
4. **Marketplace Price Erosion**:
   - Competitive selling price forced down to ₹98.0000 (`980000n`).

### 3.2 Unit Economics Breakdown Under Decay
- **Gross Selling Price**: ₹98.0000 (`980000n`).
- **Landed Cost**: ₹47.2100 (`472100n`).
- **Marketplace Fees**: Referral ₹14.7000 + Closing ₹25.0000 + FBA ₹18.0000 = ₹57.7000 (`577000n`).
- **Return & Logistics Drag**: ₹12.5000 per unit amortized.
- **Net Contribution**:
  $$\text{Net Margin} = 98.0000 - 47.2100 - 57.7000 - 12.5000 = -\text{₹}19.4100 \quad (\text{NEGATIVE})$$
- **Hurdles Breached**: Net margin is negative, RoWC is negative, return drag exceeds threshold.

### 3.3 Expected Deterministic Engine Output
```json
{
  "decision": "DO_NOT_ALLOCATE_CAPITAL",
  "execution_mode": "PAPER_SIMULATION",
  "product_id": "prod:din3017:ss304:pack-10",
  "rejection_reasons": [
    "E-M4-MARGIN-BELOW-HURDLE: Net margin -19.81% below hurdle 20.00%",
    "E-M4-HURDLE-BREACHED: Annualized RoWC -206.63% below hurdle 15.00%",
    "E-M4-RETURN-DRAG-EXCEEDED: Customer return drag ₹12.5000 exceeds threshold limit ₹5.0000",
    "E-M4-DOWNSIDE-BUFFER-EXHAUSTED: Breakeven price exceeds current marketplace selling price"
  ],
  "quarantine_recommended": false,
  "edge_decay_detected": true
}
```

---

## 4. Scenario C — Insufficient / Unauthenticated Evidence (`FAIL_CLOSED_REJECT`)

### 4.1 Defective Evidence Injection Parameters
1. **Invalid Attester Signature / Unverified Input**:
   - Supplier quote claim modified after signing or signed with an unrecognized private key (`is_verified: false`).
2. **Stale Evidence Timestamp**:
   - Freight quote capture timestamp is `2026-08-01T00:00:00Z` ($> 75\text{ days}$ old, exceeding `ttl_seconds: 604800`).
3. **Missing Mandatory Evidence**:
   - Packaging specification claim omitted entirely; no tariff provided for polybagging.

### 4.2 Ingestion & Attestation Behavior
- **Cryptographic Gate**: Detects unverified or forged provenance envelope (`is_verified === false`).
- **Freshness Gate**: Detects staleness beyond allowable TTL ($t_{\text{current}} - t_{\text{observed}} > \text{ttl\_seconds}$).
- **Completeness Gate**: Detects missing packaging cost input.
- **Fail-Closed Guarantee**: The engine **MUST NOT** substitute default assumptions, hallucinate missing values, or proceed with incomplete data.

### 4.3 Expected Deterministic Engine Output
```json
{
  "decision": "DO_NOT_ALLOCATE_CAPITAL",
  "execution_mode": "FAIL_CLOSED_REJECT",
  "product_id": "prod:din3017:ss304:pack-10",
  "rejection_reasons": [
    "E-M4-UNVERIFIED-INPUT: Claim supp:in:mumbai:metalcraft-ltd failed cryptographic signature verification",
    "E-M4-STALE-EVIDENCE: Freight quote age 75 days exceeds maximum TTL 7 days",
    "E-M4-MANDATORY-EVIDENCE-INCOMPLETE: Missing mandatory packaging_cost_claim"
  ],
  "quarantine_recommended": true,
  "edge_decay_detected": false
}
```

---

## 5. Summary Matrix of Scenario Outcomes

| Evaluation Dimension | Scenario A (Viable) | Scenario B (Edge Decay) | Scenario C (Defective Evidence) |
| :--- | :--- | :--- | :--- |
| **Evidence Validity** | Complete & Verified | Complete & Verified | **Defective / Unverified / Stale** |
| **Landed Cost** | ₹38.2100 | ₹47.2100 | Uncomputable |
| **Selling Price** | ₹105.0000 | ₹98.0000 | ₹105.0000 (listing present) |
| **Net Contribution** | +₹16.8517 (44.10%) | -₹19.4100 (-19.81%) | Undefined |
| **Cash-Conversion Cycle** | 35 days | Undefined (loss) | Undefined |
| **Annualized RoWC** | 459.90% | Negative | Undefined |
| **Decision Output** | **`ALLOCATE_CAPITAL`** | **`DO_NOT_ALLOCATE_CAPITAL`** | **`DO_NOT_ALLOCATE_CAPITAL`** |
| **Status Disposition** | Paper Execution Ready | Economic Decay Rejection | **Fail-Closed Quarantine** |

---

## 6. Gate M4.1 Addendum: Remediation of Statutory Tax & Unit Economics (OD-06)

Under Decision OD-06, the unit economics are statutorily hardened to include 18% GST on marketplace fees (with 100% ITC), Section 52 TCS & Section 194-O TDS computed on the ex-GST revenue base (₹88.9830), non-fungible separation of Income Tax TDS from GSTR-3B GST liability, and explicit supplier payment terms in the CCC formula.

### Reconciled Statutory Unit Economics Comparison

| Parameter | Scenario A Baseline (Advance EXW) | Scenario A (15-Day Trade Credit) | Scenario B (Deterioration & Decay) |
| :--- | :--- | :--- | :--- |
| **Gross Selling Price** | ₹105.0000 (`1050000n`) | ₹105.0000 (`1050000n`) | ₹98.0000 (`980000n`) |
| **Landed Cost** | ₹38.2100 (`382100n`) | ₹38.2100 (`382100n`) | ₹47.2100 (`472100n`) |
| **Total Marketplace Fees** | ₹39.7500 (`397500n`) | ₹39.7500 (`397500n`) | ₹57.7000 (`577000n`) |
| **Marketplace Fee GST (18%)** | ₹7.1550 (`71550n`) | ₹7.1550 (`71550n`) | ₹10.3860 (`103860n`) |
| **Sec 52 TCS (1% ex-GST)** | ₹0.8898 (`8898n`) | ₹0.8898 (`8898n`) | ₹0.8305 (`8305n`) |
| **Sec 194-O TDS (1% ex-GST)** | ₹0.8898 (`8898n`) | ₹0.8898 (`8898n`) | ₹0.8305 (`8305n`) |
| **Net Marketplace Disb.** | ₹56.3154 (`563154n`) | ₹56.3154 (`563154n`) | ₹28.2530 (`282530n`) |
| **Net GST Cash Settlement** | ₹2.1435 (`21435n`) | ₹2.1435 (`21435n`) | ₹0.0000 (`0n`, excess ITC) |
| **Return & Quarantine Drag** | ₹1.3242 (`13242n`) | ₹1.3242 (`13242n`) | ₹12.6736 (`126736n`) |
| **Unit Net Contribution** | **+₹14.6377 (`146377n`)** | **+₹14.6377 (`146377n`)** | **-₹31.6306 (`-316306n`)** |
| **Cash Margin** | **+38.30% (3,830 bps)** | **+38.30% (3,830 bps)** | **-66.99% (-6,699 bps)** |
| **Payment Terms (DPO)** | 0 days (Advance EXW) | 15 days (Trade credit) | 0 days |
| **Cash-Conversion Cycle** | **35 days** ($7 + 14 + 14 - 0$) | **20 days** ($7 + 14 + 14 - 15$) | **35 days** |
| **Annualized RoWC** | **+399.41% (39,941 bps)** | **+698.97% (69,897 bps)** | **-698.61% (-69,861 bps)** |
| **Decision** | **`ALLOCATE_CAPITAL`** | **`ALLOCATE_CAPITAL`** | **`DO_NOT_ALLOCATE_CAPITAL`** |

