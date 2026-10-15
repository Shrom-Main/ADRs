# POC-001 — Gate M4 Acceptance Test Scenario: DIN 3017 SS304 Hose-Clamp Vertical Slice

| Document Attribute | Specification Record |
| :--- | :--- |
| **Document Identifier** | `POC-001_Gate_M4_SS304_Vertical_Slice_Test_Scenario` |
| **Milestone Gate** | **Gate M4** — End-to-End Research & Capital-Allocation Acceptance Gate |
| **Document Status** | `PROPOSED / FOR OWNER REVIEW` |
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
└───────────────────────────────┴─────────────────────────────────────────────────┘
```

---

## 2. Scenario A — Viable Arbitrage Opportunity (`ALLOCATE_CAPITAL`)

### 2.1 Input Evidence & Cryptographic Provenance
1. **Supplier Quote Claim (`CLAIM-SUPP-001`)**:
   - Supplier: `supp:in:mumbai:metalcraft-ltd` (Registered trust anchor).
   - Timestamp: `2026-10-15T08:00:00Z` (fresh, age 2 hours).
   - Wholesale price: ₹25.0000 per pack (`250000n` subunits).
   - MOQ: 500 packs; Payment terms: Net 15 days; Incoterms: EXW Mumbai.
   - Provenance: Valid Ed25519 signature over canonical JCS payload.
2. **Inbound Logistics & Customs/Inspection Tariff (`CLAIM-LOG-001`)**:
   - Carrier: `log:in:bluedart-surface` (Registered freight anchor).
   - Freight cost: ₹4.5000 per pack (`45000n`).
   - Insurance & handling: ₹1.0000 per pack (`10000n`).
   - Inspection & customs/GST netting fee: ₹4.5100 per pack (`45100n`).
3. **Packaging & Kitting Claim (`CLAIM-PKG-001`)**:
   - Packaging contractor: ₹3.2000 per pack (`32000n`).
4. **Marketplace Listing & Fee Schedule Claim (`CLAIM-MKT-001`)**:
   - Marketplace: Amazon.in FBA (`amzn:in:asin:B09XYZ1234`).
   - Gross retail selling price: ₹105.0000 per pack (`1050000n`).
   - Referral fee: 15.00% = ₹15.7500 (`157500n`).
   - Closing fee: ₹10.0000 (`100000n`).
   - FBA pick & pack / weight handling: ₹14.0000 (`140000n`).
   - Total marketplace fees: ₹39.7500 (`397500n`).

### 2.2 Financial & Tax Arithmetic Execution
- **Exact Landed Cost**:
  $$\text{Landed Cost} = 25.0000 + 4.5000 + 3.2000 + 1.0000 + 4.5100 = \text{₹}38.2100 \quad (382100n \text{ subunits})$$
- **Net Merchant Proceeds**:
  $$\text{Gross Revenue} - \text{Total Marketplace Fees} = 105.0000 - 39.7500 = \text{₹}65.2500 \quad (652500n)$$
- **GST & Tax Settlement**:
  - Output GST liability on sale: ₹16.0169 (18% inclusive in ₹105.00).
  - Input Tax Credit (ITC) on procurement & freight: ₹5.8286.
  - Net GST payable: ₹10.1883.
- **Unit Net Margin (After Tax & All Fees)**:
  $$\text{Net Contribution} = 65.2500 - 38.2100 - 10.1883 = \text{₹}16.8517 \quad (168517n)$$
  $$\text{Cash-on-Cash Return} = \frac{16.8517}{38.2100} = 44.10\% \quad (> 20.00\% \text{ hurdle})$$
- **Outlay Recovery Duration**:
  - Procurement outlay: Day 0; Fulfillment & clearing: Day 18; Lifecycle recovery: 18 days ($\le 30\text{ days}$).
  - Annualized RoPF: $\approx 89.4\%$ ($> 25.00\%$ hurdle).

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
    "projected_outlay_recovery_days": 18,
    "downside_price_buffer_bps": 2250
  },
  "constraint_evaluations": {
    "evidence_provenance_verified": true,
    "landed_cost_within_bounds": true,
    "margin_above_hurdle": true,
    "ropf_above_hurdle": true,
    "recovery_duration_acceptable": true
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
3. **Elevated Return Rate Drag**:
   - Customer return rate spikes to 16.00% (from nominal 2.00%), incurring unrecoverable reverse logistics fees and damaged packaging repackaging write-offs.
4. **Marketplace Price Erosion**:
   - Competitive selling price forced down to ₹98.0000 (`980000n`).

### 3.2 Unit Economics Breakdown Under Decay
- **Gross Selling Price**: ₹98.0000 (`980000n`).
- **Landed Cost**: ₹47.2100 (`472100n`).
- **Marketplace Fees**: Referral ₹14.7000 + Closing ₹25.0000 + FBA ₹18.0000 = ₹57.7000 (`577000n`).
- **Return & Logistics Drag**: ₹6.5000 per unit amortized.
- **Net Contribution**:
  $$\text{Net Margin} = 98.0000 - 47.2100 - 57.7000 - 6.5000 = -\text{₹}13.4100 \quad (\text{NEGATIVE})$$
- **Hurdle Breached**: Margin ($< 0\%$) and RoPF ($< 0\%$) completely breached.

### 3.3 Expected Deterministic Engine Output
```json
{
  "decision": "DO_NOT_ALLOCATE_CAPITAL",
  "execution_mode": "PAPER_SIMULATION",
  "product_id": "prod:din3017:ss304:pack-10",
  "rejection_reasons": [
    "E-ERR-051: NET_MARGIN_BELOW_HURDLE (actual: -13.68%, hurdle: 20.00%)",
    "E-ERR-052: ROPF_NEGATIVE (actual: -34.12%, hurdle: 25.00%)",
    "E-ERR-053: RETURN_DRAG_EXCEEDED (actual: 16.00%, limit: 5.00%)",
    "E-ERR-054: DOWNSIDE_BUFFER_EXHAUSTED"
  ],
  "quarantine_recommended": false,
  "edge_decay_detected": true
}
```

---

## 4. Scenario C — Insufficient / Unauthenticated Evidence (`FAIL_CLOSED_REJECT`)

### 4.1 Defective Evidence Injection Parameters
1. **Invalid Attester Signature**:
   - Supplier quote claim modified after signing (e.g. unit price altered from ₹30.00 to ₹25.00) or signed with an unknown private key not registered in `TrustAnchorRegistry`.
2. **Stale Evidence Timestamp**:
   - Freight quote capture timestamp is `2026-08-01T00:00:00Z` ($> 75\text{ days}$ old, exceeding the 7-day freshness policy limit).
3. **Missing Mandatory Evidence**:
   - Packaging specification claim omitted entirely; no tariff provided for polybagging.

### 4.2 Ingestion & Attestation Behavior
- **Cryptographic Gate**: Ed25519 signature verification fails on modified claim payload.
- **Freshness Gate**: Timestamp validator detects staleness beyond allowed window.
- **Completeness Gate**: Financial calculation pipeline detects missing packaging cost input.
- **Fail-Closed Guarantee**: The engine **MUST NOT** substitute default assumptions, hallucinate missing values, or proceed with incomplete data.

### 4.3 Expected Deterministic Engine Output
```json
{
  "decision": "DO_NOT_ALLOCATE_CAPITAL",
  "execution_mode": "FAIL_CLOSED_REJECT",
  "product_id": "prod:din3017:ss304:pack-10",
  "rejection_reasons": [
    "E-ERR-001: CLAIM_SIGNATURE_INVALID (attester: supp:in:mumbai:metalcraft-ltd)",
    "E-ERR-007: CLOCK_SKEW_OR_STALENESS_EXCEEDED (freight quote age: 75 days, max: 7 days)",
    "E-ERR-047: MANDATORY_EVIDENCE_INCOMPLETE (missing packaging_cost_claim)"
  ],
  "quarantine_recommended": true,
  "edge_decay_detected": false
}
```

---

## 5. Summary Matrix of Scenario Outcomes

| Evaluation Dimension | Scenario A (Viable) | Scenario B (Edge Decay) | Scenario C (Defective Evidence) |
| :--- | :--- | :--- | :--- |
| **Evidence Validity** | Complete & Verified | Complete & Verified | **Defective / Unauthenticated** |
| **Landed Cost** | ₹38.2100 | ₹47.2100 | Uncomputable |
| **Selling Price** | ₹105.0000 | ₹98.0000 | ₹105.0000 (listing present) |
| **Net Contribution** | +₹16.8517 (44.10%) | -₹13.4100 (-13.68%) | Undefined |
| **Outlay Recovery** | 18 days | Undefined (loss) | Undefined |
| **Decision Output** | **`ALLOCATE_CAPITAL`** | **`DO_NOT_ALLOCATE_CAPITAL`** | **`DO_NOT_ALLOCATE_CAPITAL`** |
| **Status Disposition** | Paper Execution Ready | Economic Decay Rejection | **Fail-Closed Quarantine** |
