I've completed the independent multidisciplinary technical review of **POC-001 (Market HFT OS)** across both repository snapshots (`Market-HFT-OS` at `a1bd3599e21dfb79e45df3e6c189d18c781fc5cb` and `ADRs` at `c52f66854b695320a0f5ffb0144c29bf72c91e38`) and generated the two self-contained Antigravity review notes in Canvas:

* **`ARGON_REVIEW_NOTE_MARKET_HFT_OS.md`**: Implementation, financial engine, cryptography, persistence, security, and test-engineering review note for `Market-HFT-OS`.
* **`ARGON_REVIEW_NOTE_ADRS.md`**: Specification errata, governance hierarchy, conformance report audit, and cross-repository synchronization review note for `ADRs`.

### Output 1 — Audit Context, Source Manifest & Discrepancy Register

#### 1.1 Repository Baseline & Source Manifest

| Attribute | `Market-HFT-OS` (Implementation) | `ADRs` (Specifications & Audit Evidence) |
| --- | --- | --- |
| **Audit Timestamp (UTC)** | `2026-10-14T12:14:57Z` (Local: `2026-10-14T17:41:37+05:30`) | `2026-10-14T12:14:57Z` (Local: `2026-10-14T17:41:37+05:30`) |
| **Canonical GitHub URL** | `[https://github.com/Shrom-Main/Market-HFT-OS](https://github.com/Shrom-Main/Market-HFT-OS)` | `[https://github.com/Shrom-Main/ADRs](https://github.com/Shrom-Main/ADRs)` |
| **Default Branch** | `main` (per `PROJECT_CHARTER.md` & `scripts/sync_repos.py`) | `main` (per `README.md` & `scripts/sync_repos.py`) |
| **Exact HEAD Commit SHA** | `a1bd3599e21dfb79e45df3e6c189d18c781fc5cb` (`a1bd359`) | `c52f66854b695320a0f5ffb0144c29bf72c91e38` (`c52f668`) |
| **Latest Archive Timestamp** | `2026-10-14T10:32:35Z` | `2026-10-14T10:34:53Z` |
| **Prior Commit Lineage (from Reports)** | `582637b` (M0) $\to$ `abfaa04` $\to$ `70121a0` (M1) $\to$ `5c7b30f` $\to$ `838c7b5` $\to$ `befe4df` $\to$ `3df48e4` $\to$ `9a61e0e` $\to$ `d238774` $\to$ `da62382` $\to$ `cbafb60` (M2) $\to$ `9ce7cfa` $\to$ `98922db` $\to$ `58c66e5` $\to$ `7415c61` $\to$ `8a89cf0` $\to$ `a1bd359` (M3 HEAD) | `77eff71c3807c8852b49355f50e814bd75eb90ad` (M1 Spec Freeze) $\to$ `c52f66854b695320a0f5ffb0144c29bf72c91e38` (M3 Addendum HEAD) |
| **Frozen Spec Version & Hashes** | `AG/POC-001_Gate_M1_Design_Readiness_Specification.md` (v1.13 Final, LF line endings, Git blob `6a95577a689259f4ad7c22caad00c691493afe7a`, SHA-256 `c52fe522342716853de745bb5523492bc16b872f5a7ac2a65ca44e38d06239ff`) | `POC-001_Gate_M1_Design_Readiness_Specification.md` (v1.13 Final, CRLF line endings, Git blob `ac8899da3a6dcccb2c612247302e6f57fc566472`, SHA-256 `efaa93d85edb15c7ba88ed2ab4362b2f44554832147219b3f41ec7639cf4c0a7`) |
| **Tracked Test Artifact SHA-256** | `test-results.json`: `feccb25332319938403bd3efa7623bca5d488c3545fdfdd4e898f7615e932119` (17 suites, 129 passed) | `POC-001_Gate_M3_Test_Execution_Results.json`: `feccb253...` (identical to `test-results.json`); `POC-001_Gate_M2_Test_Execution_Results.json`: `49001a4a...` (15 suites, 106 passed) |

#### 1.2 Inspected Files, Verification Commands Run & Scope Limitations

* **Files Inspected (100% of both repository archives)**:
* **`Market-HFT-OS` (50 files)**: `PROJECT_CHARTER.md`, `README.md`, `RESEARCH_CORPUS_INDEX.md`, `package.json`, `package-lock.json`, `tsconfig.json`, `vitest.config.ts`, `.gitignore`, `start_sync_daemon.bat`, `sync_now.bat`, `test-results.json`, `AG/POC-001_Gate_M1_Design_Readiness_Specification.md`, `AG/ADRXX1.pdf` (60 pp.), `AG/ADRXX2.pdf` (64 pp.), `AG/ADRXX3.pdf` (46 pp.), all 4 scripts in `scripts/` (`sync_repos.py`, `git_askpass.py`, `git_askpass.bat`, `test_crash_worker.ts`), all 19 production TypeScript modules in `src/` (`index.ts`, `canonical/allowlist.ts`, `canonical/crypto.ts`, `canonical/currency.ts`, `canonical/deterministic.ts`, `canonical/domain.ts`, `canonical/jcs.ts`, `canonical/product.ts`, `checkpoint/trustAnchor.ts`, `execution/engine.ts`, `execution/simulatedGateway.ts`, `feeds/feedHandler.ts`, `feeds/localWebSocketTransport.ts`, `feeds/streamingAdapter.ts`, `financial/cashFlowEngine.ts`, `ledger/actualsGuard.ts`, `persistence/atomicPromotion.ts`, `persistence/durableRecoveryJournal.ts`, `persistence/postgresAdapter.ts`, `portfolio/simulationPortfolio.ts`, `simulation/simulationPipeline.ts`, `verification/claims.ts`, `verification/gate.ts`), and all 17 test files in `tests/acceptance/suite01..suite16` and `tests/integration/suite17_real_postgres_integration.test.ts`.
* **`ADRs` (20 files)**: `README.md`, `.gitignore`, `POC-001_Gate_M1_Design_Readiness_Specification.md`, `POC-001_Gate_M1_Implementation_Execution_Report.md`, `POC-001_Gate_M1_Comprehensive_Conformance_Matrix_Report.md`, `POC-001_Gate_M2_Execution_and_Integration_Conformance_Report.md`, `POC-001_Gate_M2_Test_Execution_Results.json`, `POC-001_Gate_M3_Persistence_and_Crash_Recovery_Conformance_Report.md`, `POC-001_Gate_M3_WAL_Boundary_Normalization_Audit_Addendum.md`, `POC-001_Gate_M3_Test_Execution_Results.json`, `POC-001_Gate_M3_Typecheck_Execution_Results.txt`, `ADRXX3.pdf`, and `002.docx` through `009.docx`.


* **Commands & Independent Checks Executed**:
* Computed SHA-256 and Git blob (`git hash-object`) digests across every file in both archives and verified archive commit comments (`unzip -z`).
* Diffed `ADRs/POC-001_Gate_M1_Design_Readiness_Specification.md` against `Market-HFT-OS/AG/POC-001_Gate_M1_Design_Readiness_Specification.md` and rendered/extracted `ADRXX1.pdf`, `ADRXX2.pdf`, `ADRXX3.pdf`, and `002.docx`–`009.docx`.
* Executed static AST/regex cross-referencing of all exported symbols in `src/` against `tests/` and all 111 specified test IDs in Gate M1 Spec §8.1–§8.2.
* Executed an isolated, zero-dependency Node.js (`v18.20.4`) verification harness confirming our mathematical, cryptographic, sorting, and byte-accounting counterexamples without installing packages or mutating repository files.


* **Scope Limitations & Unverified Runtime Elements**:
* Both uploaded archives are `git archive` commit snapshots (`a1bd359` and `c52f668`) without `.git/` directories, `node_modules/`, `_salvage/`, or the local Windows environment (`D:\Market HFT OS`, `GithubPersonalAccessTokenFORAG.env`, or live PostgreSQL 16.8 on `localhost:5432`).
* Live GitHub URLs (`[https://github.com/Shrom-Main/Market-HFT-OS](https://github.com/Shrom-Main/Market-HFT-OS)` and `[https://github.com/Shrom-Main/ADRs](https://github.com/Shrom-Main/ADRs)`) are private or restricted from unauthenticated web browsing.
* Per Section 3 review boundaries (and offline sandbox constraints), we did not run `npm ci`, `vitest`, `tsc`, or connect to a live PostgreSQL instance (`esbuild@0.28.2` and `fsevents@2.3.3` in `package-lock.json` declare `hasInstallScript: true`, and `suite16` / `sync_repos.py` mutate disk or git state).



#### 1.3 Current-State & Governance Discrepancy Register

| Discrepancy ID | Conflicting Statements & Exact Sources | Conflict Type | Controlling Source & Safest Interim Interpretation | Owner Decision / Evidence Required to Resolve |
| --- | --- | --- | --- | --- |
| **DISC-01** | **Statement A:** `Market-HFT-OS/PROJECT_CHARTER.md` (v0.2.4, L4–L8, §12 L320–L335) states `Document Status: PROPOSED — awaiting project-owner approval` and `Operating Mode: Strict Read-Only prior to Gate M0 authorization`.<br>

<br>**Statement B:** `ADRs/POC-001_Gate_M1_Design_Readiness_Specification.md` (v1.13 Final, L4, §1.1 L51) states `awaiting Project Owner Design Freeze` and `Implementation Status: BLOCKED`.<br>

<br>**Statement C:** `ADRs/POC-001_Gate_M1_Implementation_Execution_Report.md` (§1 L13) and `M2`/`M3` reports state Gate M1 Design Freeze was unconditionally approved at commit `77eff71` and implementation is authorized through Gate M3. | Governance & Documentary | **Controlling Source:** Explicit Project Owner gate approvals (`PROJECT_CHARTER.md` §10.1).<br>

<br>**Interim Interpretation:** Least-privilege read-only audit posture; treat M1–M3 code as reviewable candidate artifacts, not self-authorizing amendments to the Charter or Frozen Spec. | Record a formal `GATE_AUTHORIZATION_LEDGER.md` in `ADRs` with owner sign-offs for Gates M0–M3 and update document status headers in `PROJECT_CHARTER.md` and `POC-001_Gate_M1_Design_Readiness_Specification.md`. |
| **DISC-02** | **Statement A:** `ADRs/POC-001_Gate_M3_Persistence_and_Crash_Recovery_Conformance_Report.md` Header (L6–L8), §1.4 (L38–L41), §2 (L52), and §3 (L62–L94) state baseline is `7415c61`, `NATIVE POSTGRES OPEN (CONDITIONALLY GATED)`, `123 passed, 3 skipped (126 total)`, and `Suite 17: 1/4 passed (3 skipped)`.<br>

<br>**Statement B:** Sections 4.4 (L152–L169) and 5 (L173–L185) of the **same file** and `POC-001_Gate_M3_WAL_Boundary_Normalization_Audit_Addendum.md` state baseline is `a1bd359 (unpushed)` with `129 passed, 0 skipped` and `Suite 17: 6/6 passed` on PostgreSQL 16.8.<br>

<br>**Statement C:** `Market-HFT-OS/README.md` (L7, L49, L55, L80) states `Gate_M3_Preflight-Passing_(116_Tests)` across `16 test files` (`suite16` = 10 tests, `suite17` omitted). | Operational & Documentary | **Controlling Source:** Actual repository tree at `a1bd359` (`test-results.json` has 17 suites / 129 tests; `suite17` is conditionally gated on `DATABASE_URL`).<br>

<br>**Interim Interpretation:** Sections 1–3 of the M3 Conformance Report and `Market-HFT-OS/README.md` are stale; live PostgreSQL results in `test-results.json` are unverified in our offline audit environment. | Reconcile `POC-001_Gate_M3_Persistence_and_Crash_Recovery_Conformance_Report.md` and `Market-HFT-OS/README.md` to a single truthful baseline and commit state. |
| **DISC-03** | **Statement A:** `ADRs/POC-001_Gate_M1_Design_Readiness_Specification.md` §3.2 (`GatewayClaimEndorsementReceipt`, L763) and §6.2 (`KAT-05B`, L2464) require `claim_signing_payload_sha256` to equal the SHA-256 of the full `ClaimSigningPayload`.<br>

<br>**Statement B:** §3.3 of the **same specification** (`L1613`, `L1716`) checks `rcpt.claim_payload_digest !== params_sha256` (`claim_parameters` hash only).<br>

<br>**Statement C:** `Market-HFT-OS/src/verification/gate.ts` (L473–L477) and `src/persistence/atomicPromotion.ts` (L251–L256) combine both fields with `||`, resulting in a tautological bypass in `atomicPromotion.ts` and cross-offer replay in `gate.ts`. | Architectural, Specification & Security | **Controlling Source:** Gate M1 Core Invariant 3 & §3.2 (`KAT-05B`) — receipts must cryptographically bind the offer, product, evidence, attester, and role.<br>

<br>**Interim Interpretation:** Treat §3.3 `params_sha256` as a specification defect and the implementation's `||` check as a critical security vulnerability (`ARGON-CRYPTO-001`). | Owner approval of Gate M1 Specification Erratum v1.14 unifying §3.2 and §3.3 on `claim_signing_payload_sha256 === sha256(canonicalizeJCS(ClaimSigningPayload))`. |
| **DISC-04** | **Statement A:** All reports cite `POC-001_Gate_M1_Design_Readiness_Specification.md` as pinned to Git blob `ac8899da3a6dcccb2c612247302e6f57fc566472`.<br>

<br>**Statement B:** `ADRs/POC-001_Gate_M1_Design_Readiness_Specification.md` has blob `ac8899da...` (CRLF, SHA-256 `efaa93d8...`), whereas `Market-HFT-OS/AG/POC-001_Gate_M1_Design_Readiness_Specification.md` has blob `6a95577a...` (LF, SHA-256 `c52fe522...`), alongside superseded PDFs `ADRXX1.pdf` and `ADRXX2.pdf`. | Documentary & Repository Hygiene | **Controlling Source:** `ADRs/POC-001_Gate_M1_Design_Readiness_Specification.md` (matches pinned blob `ac8899da...`). | Remove duplicate/superseded specification files in `Market-HFT-OS/AG/` or enforce identical line endings via `.gitattributes`. |
| **DISC-05** | **Statement A:** `ADRs/POC-001_Gate_M1_Comprehensive_Conformance_Matrix_Report.md` claims full Gate M1 specification conformance across `AUDIT-01`–`AUDIT-52`.<br>

<br>**Statement B:** 73 of the 111 test cases specified in Gate M1 Spec §8.1–§8.2 (and 7 exported functions in `src/`) have zero test invocations, and core spec modules (Two-Tier Gross-Clearing `B_clearing`/`B_bank`, XIRR solver, `PO_AMENDED`, `SIM-GUARD-002` `E-ERR-025`, and `OfferStreamEvent` hash chaining) are unimplemented. | Architectural & Verification | **Controlling Source:** Gate M1 Spec §8.0 Three-State Conformance Rule (prohibits promoting states without runtime evidence). | Downgrade unverified/unimplemented items in the conformance matrix and implement missing contracts and tests before gate advancement. |

### Output 2 — Executive Assessment

* **Overall Assessment & Confidence**: **High confidence** that `POC-001` at `Market-HFT-OS` commit `a1bd359` and `ADRs` commit `c52f668` contains **material financial-calculation, cryptographic-verification, persistence-recovery, simulation-accounting, and operational-security defects**, as well as internal contradictions within both the frozen Gate M1 specification and the Gate M3 conformance report.
* **Most Consequential Defects**:
1. **Tautological Gateway Receipt Revalidation & Cross-Offer Replay (`ARGON-CRYPTO-001`, Critical)**: In `src/persistence/atomicPromotion.ts` (L251–L256), post-lock digest revalidation compares `rcpt.claim_signing_payload_sha256` against itself (`expectedPayloadDigest !== rcpt.claim_signing_payload_sha256`) whenever `claim_payload_digest` is omitted, rendering `AUDIT-47` a no-op. In `src/verification/gate.ts` (L473–L477), accepting `params_sha256` allows a receipt issued for one offer/product to be replayed onto another offer/product, and `rcpt.operator_id` / `rcpt.operator_role` are never matched against the claim's `attester_id` / `claimed_role`. Notice also that `GATEWAY_CLAIM_ENDORSEMENT` has **0 test executions** across all 17 test suites.
2. **Unauthenticated FX Oracle Public Keys & 96,111x FX Decimal-Scale Misparsing (`ARGON-FIN-001`, Critical)**: `validateFXReceiptAtPointOfUse` (`src/canonical/currency.ts`, L106–L130) verifies signatures using `receipt.oracle_public_key_hex` directly from the untrusted receipt without checking any authority registry. Meanwhile, `convertMoneySubunitsExact` (L63) strips the decimal point via `rateDecimal.replace('.', '')` without checking fractional digit count against `rateScale`, causing `"86.5"` at `rateScale = 6` to undervalue currency conversions by a factor of $10^5$.
3. **Compromised & Revoked Attester Keys Fail Open (`ARGON-CRYPTO-002`, High)**: `validateAttesterAuthority` (`src/verification/claims.ts`, L344–L352) nests `if (principal.compromised)` inside `if (principal.revoked)` and fails open when `revoked_at_utc` is omitted.
4. **Evidence Allowlist (`validateEvidenceAllowlistEligibility`) Never Called in Promotion Pipeline (`ARGON-EVID-001`, High)**: The 18-tuple allowlist in `src/canonical/allowlist.ts` is never imported or called by `gate.ts` or `atomicPromotion.ts`, and `ResolvedEvidenceEnvelope` omits evidence kind and document type.
5. **Floating-Point Financial Engine, Inverted Timestamp Sort, Missing Two-Tier Clearing & Missing XIRR Solver (`ARGON-FIN-002`, High)**: `src/financial/cashFlowEngine.ts` uses IEEE 754 `number` instead of `CanonicalMoney`/`bigint`, fails open on `NaN`, sorts ISO-8601 strings lexicographically (`'2026-10-10T10:00:00.500Z' < '2026-10-10T10:00:00Z'`, inverting intra-second order), allows negative `fulfillPO` amounts to inflate committed capital, and omits both the Two-Tier Gross-Clearing model (`B_clearing` vs `B_bank`) and the XIRR solver.
6. **WAL Blank-Line Truncation Corruption, Boundary 3 Double-Counting & Poisoned Recovery Mutation (`ARGON-PERSIST-001`, High)**: `FileBackedDurableRecoveryJournal` (`src/persistence/durableRecoveryJournal.ts`, L220) skips blank-line bytes when computing `validBytesLength`, causing torn-tail `ftruncateSync` to slice into valid records; `CrashRecoveryEngine.recoverDurable` (L575–L628) double-counts Boundary 3 fills in both `recovered_fills_count` and `skipped_duplicate_fills_count` and mutates `portfolio` in memory before checking whether the WAL journal is poisoned.
7. **Infinite Offer Inventory Synthesis & Same-Millisecond Tick Collision in Simulation Pipeline (`ARGON-SIM-001`, High)**: `SimulationPipeline.processMarketEvent` (`src/simulation/simulationPipeline.ts`, L138–L215) never decrements `offer.available_quantity` across fills, and `DryRunExecutionEngine` (`src/execution/engine.ts`, L73) keys `intent_id` solely by millisecond timestamp, crashing on same-millisecond ticks.


* **Milestone Readiness**: The next milestone is **BLOCKED**. Targeted, modular remediations (not a full rewrite) and a Gate M1 Specification Erratum (`v1.14`) are required before Gate M3 can be closed.

### Output 3 — Deduplicated Findings Register

#### 3.1 Confirmed Defects (Implementation & Security)

1. **`ARGON-CRYPTO-001` — Tautological Post-Lock Digest Revalidation, Parameter-Only Digest Replay & Unbound Gateway Operator Identity**
* **Severity / Confidence**: Critical / High
* **Category & Affected Gate**: Evidence Cryptography & Promotion Gates (Gate M1 / Gate M3)
* **Location**: `Market-HFT-OS` (`a1bd359`), `src/persistence/atomicPromotion.ts` (`commitPromotionIfVersionAndConsumeNonces`, L247–L257), `src/verification/gate.ts` (`evaluateOfferPromotionReadOnly`, L469–L505), `src/verification/claims.ts` (`validateGatewayEndorsementReceipt`, L236–L300)
* **Violated Requirement**: Gate M1 Spec §1 Invariants 3 & 6, §3.2 (`GatewayClaimEndorsementReceipt`), §4.1 (`AUDIT-47`, `AUDIT-51`).
* **Failure Mechanism & Minimal Counterexample**:
* In `src/persistence/atomicPromotion.ts` L251–L256:
```typescript
const expectedPayloadDigest =
    rcpt.claim_payload_digest || rcpt.claim_signing_payload_sha256;
const param_canonical_bytes =
    Buffer.from(canonicalizeJCS(claim.claim_parameters), 'utf8');
const expected_param_digest = sha256(param_canonical_bytes);
if (expectedPayloadDigest !== expected_param_digest &&
    expectedPayloadDigest !== rcpt.claim_signing_payload_sha256) {
  throw new Error(
      `E-ERR-017: DIGEST_BINDING_MISMATCH: ...`);
}

```


When `rcpt.claim_payload_digest` is `undefined` (as in `KAT-05B`), `expectedPayloadDigest` equals `rcpt.claim_signing_payload_sha256`, making `expectedPayloadDigest !== rcpt.claim_signing_payload_sha256` identically `false`.
* In `src/verification/gate.ts` L475, `expectedPayloadDigest !== actualDigest && expectedPayloadDigest !== params_sha256` accepts `params_sha256` (which hashes only `claim_parameters`), omitting `offer_id`, `product_id`, `evidence_id`, `evidence_sha256`, `attester_id`, `claimed_role`, and `attested_at_utc`.
* Neither `validateGatewayEndorsementReceipt`, `evaluateOfferPromotionReadOnly`, nor `commitPromotionIfVersionAndConsumeNonces` checks `rcpt.operator_id === claim.attestation.attester_id` or `rcpt.operator_role === claim.attestation.claimed_role`.


* **Consequence**: A valid gateway receipt issued for one offer, product, or operator can be attached to a different offer, product, or operator claim without detection.
* **Recommended Remediation**: Remove `claim_payload_digest` and `params_sha256` fallback; require `rcpt.claim_signing_payload_sha256 === sha256(Buffer.from(canonicalizeJCS(validateAndBuildClaimSigningPayload(offer.offer_id, offer.product_id, claim)), 'utf8'))` and `rcpt.operator_id === claim.attestation.attester_id && rcpt.operator_role === claim.attestation.claimed_role` in both Phase 1 (`gate.ts`) and Phase 2 (`atomicPromotion.ts`).
* **Regression Test / Closure Criterion**: Add `GATEWAY-DIGEST-BIND-OFFER-REPLAY` and `GATEWAY-OPERATOR-ROLE-MISMATCH` to `suite03`/`suite05` proving `E-ERR-017` is thrown when a gateway receipt is replayed across offers or operators.
* **Verification Status**: Independently verified via static analysis and Node.js counterexample harness (`verify_counterexamples.mjs`).


2. **`ARGON-FIN-001` — Unauthenticated Self-Asserted FX Oracle Key & Unvalidated `rateDecimal` Scale in FX Conversion**
* **Severity / Confidence**: Critical / High
* **Category & Affected Gate**: Financial Mathematics & Cryptographic Oracle Verification (Gate M1)
* **Location**: `Market-HFT-OS` (`a1bd359`), `src/canonical/currency.ts` (`convertMoneySubunitsExact`, L49–L90; `validateFXReceiptAtPointOfUse`, L106–L130)
* **Violated Requirement**: Gate M1 Spec §1 Invariants 12 & 13, §2.1 (`AUDIT-10`, `AUDIT-11`).
* **Failure Mechanism & Minimal Counterexample**:
* `validateFXReceiptAtPointOfUse` L127 calls `ed25519Verify(unsigned_bytes, receipt.oracle_public_key_hex, oracle_signature)` without verifying that `receipt.oracle_public_key_hex` belongs to a registered, unrevoked, uncompromised `CRYPTOGRAPHIC_ORACLE` in `PRINCIPAL_AUTHORITY_REGISTRY` (or a dedicated `FX_ORACLE_REGISTRY`).
* `convertMoneySubunitsExact` L63 executes `const rateNumerator = BigInt(rateDecimal.replace('.', ''));` without validating `rateDecimal` format, sign, or fractional digit length against `rateScale`, and without calling `createCanonicalMoney` on `source`. Calling `convertMoneySubunitsExact(createCanonicalMoney('10000', 'USD', 4), 'INR', '86.5', 6, 4)` produces `'9'` (`0.0009 INR`) instead of `'865000'` (`86.5000 INR`) — a **96,111x undervaluation**.


* **Consequence**: Complete compromise of cross-currency valuation and silent orders-of-magnitude corruption when FX rate strings omit trailing zeros.
* **Recommended Remediation**: Validate `source` via `createCanonicalMoney`; parse `rateDecimal` using a strict positive decimal validator enforcing exact fractional scale `rateScale` (or padding/rejecting via `parseDecimalPriceToSubunits` with positivity check `rateNumerator > 0n`); authenticate `receipt.oracle_public_key_hex` against a trusted oracle registry with validity window, revocation, and compromise checks.
* **Regression Test / Closure Criterion**: Negative tests rejecting unregistered/revoked/compromised oracle keys (`E-ERR-008`), non-positive FX rates, and mismatched fractional digit scales.
* **Verification Status**: Independently verified via static analysis and Node.js execution (`verify_counterexamples.mjs`).


3. **`ARGON-CRYPTO-002` — `validateAttesterAuthority` Fails Open on Compromised Keys (`revoked: false, compromised: true`) and Revoked Keys Missing `revoked_at_utc**`
* **Severity / Confidence**: High / High
* **Category & Affected Gate**: Evidence Cryptography & Authority Validation (Gate M1)
* **Location**: `Market-HFT-OS` (`a1bd359`), `src/verification/claims.ts` (`validateAttesterAuthority`, L344–L352); also embedded in `ADRs/POC-001_Gate_M1_Design_Readiness_Specification.md` (§3.2, L1038–L1046)
* **Violated Requirement**: Gate M1 Spec §3.2 (`AUDIT-05`, `RegisteredPrincipal.compromised`: *"If true, retroactively invalidates all signatures"*).
* **Failure Mechanism & Minimal Counterexample**:
```typescript
if (principal.revoked) {
  if (principal.compromised) {
    throw new Error('E-ERR-019: OPERATOR_KEY_REVOKED: Principal key compromised (retroactive invalidation)');
  }
  const revoked_ms = Date.parse(principal.revoked_at_utc || '');
  if (!isNaN(revoked_ms) && attested_ms >= revoked_ms) {
    throw new Error('E-ERR-019: OPERATOR_KEY_REVOKED: Attestation signed at or after key revocation timestamp');
  }
}

```


Passing `{ revoked: false, compromised: true }` or `{ revoked: true, revoked_at_utc: undefined }` returns the `principal` without throwing.
* **Consequence**: Compromised or improperly revoked operator keys remain accepted for signing promotion claims.
* **Recommended Remediation**: Check `if (principal.compromised) throw new Error('E-ERR-019: ...');` unconditionally before `if (principal.revoked)`, and when `principal.revoked` is true, require `principal.revoked_at_utc` to pass `validateIso8601UtcTimestamp` (throwing `E-ERR-019` if absent or malformed), matching `validateGatewayEndorsementReceipt` (L282–L292) and `verifyStreamCheckpointReceipt` (L82–L108).
* **Regression Test / Closure Criterion**: Add unit tests for `{ revoked: false, compromised: true }` and `{ revoked: true }` without `revoked_at_utc` asserting `E-ERR-019`.
* **Verification Status**: Independently verified via static analysis and Node.js execution (`verify_counterexamples.mjs`).


4. **`ARGON-EVID-001` — 18-Tuple Evidence Allowlist (`validateEvidenceAllowlistEligibility`) Disconnected from Offer Promotion Gate**
* **Severity / Confidence**: High / High
* **Category & Affected Gate**: Evidence Integrity & Promotion Gate (Gate M1)
* **Location**: `Market-HFT-OS` (`a1bd359`), `src/canonical/allowlist.ts` (L34–L49), `src/verification/claims.ts` (`ResolvedEvidenceEnvelope`, L141–L145), `src/verification/gate.ts` (`reconcileOfferClaims`, L32–L106; `evaluateOfferPromotionReadOnly`, L401–L553)
* **Violated Requirement**: Project Charter §3.1–§3.2 (`DEC-013`, `DEC-015`) & Gate M1 Spec §1 Invariant 1, §3.1 (`AUDIT-01`, `AUDIT-07`).
* **Failure Mechanism & Minimal Counterexample**: `validateEvidenceAllowlistEligibility` is never imported or called anywhere in `src/`. `ResolvedEvidenceEnvelope` contains only `{ evidence_id, event_sha256, provenance }` and lacks `evidence_kind`, `verification_status`, `offer_status`, and `document_type`. Thus, evidence originating from `SYNTHETIC_TEST`, `SCENARIO`, or `FORECAST` can be registered in `STREAM_EVIDENCE_REGISTRY` and used to promote an offer to `VERIFIED_EXECUTABLE_OFFER` without triggering `E-ERR-001` or `E-ERR-033`. In addition, calling `reconcileOfferClaims` directly with a missing evidence key throws an unhandled `TypeError` when dereferencing `.provenance` at L55, L73, L86, and L98.
* **Consequence**: Synthetic/scenario data can be promoted into verified executable offers, violating the core epistemic boundary of POC-001.
* **Recommended Remediation**: Include `evidence_kind`, `verification_status`, `offer_status`, and `document_type` on `ResolvedEvidenceEnvelope`, enforce `validateEvidenceAllowlistEligibility` for all 4 claims in `evaluateOfferPromotionReadOnly` and `commitPromotionIfVersionAndConsumeNonces`, and guard missing evidence lookups in `reconcileOfferClaims` with `E-ERR-012`.
* **Regression Test / Closure Criterion**: Implement `PROMO-ALLOW-REJECT-011` and `CLAIM-EVID-MISMATCH-008` in `suite03`/`suite04` against `evaluateOfferPromotionReadOnly`.
* **Verification Status**: Independently verified via static codebase inspection (`check_coverage.py`).


5. **`ARGON-FIN-002` — Floating-Point Cash Flows, Missing Two-Tier Clearing, Lexicographical Timestamp Inversion, Transient Zero-Crossing, Unvalidated PO Lifecycle & Missing XIRR Solver**
* **Severity / Confidence**: High / High
* **Category & Affected Gate**: Financial Mathematics & Accounting Invariants (Gate M1)
* **Location**: `Market-HFT-OS` (`a1bd359`), `src/financial/cashFlowEngine.ts` (L1–L320)
* **Violated Requirement**: Project Charter §2.2 (`DEC-012`, `DEC-014`) and Gate M1 Spec §1 Invariants 7–10 & 12, §7.1–§7.3 (`AUDIT-16`, `AUDIT-18`, `AUDIT-34`, `AUDIT-38`, `AUDIT-44`, `AUDIT-48`, `AUDIT-50`).
* **Failure Mechanism & Minimal Counterexamples**:
* **Float64 & `NaN` Fail-Open (L6, L68, L136)**: `OperatingCashFlowEntry.amount` is a JavaScript `number` with no `currency` field or `Number.isSafeInteger` check. Passing `[{ entry_timestamp_utc: '2026-10-10T10:00:00Z', sequence_number: 1, amount: NaN, flow_kind: 'PROCUREMENT_OUTLAY' }]` to `computePostOutlayRecoveryMetrics` returns `{ status: 'ZERO_OPERATING_OUTLAY', peak_operating_funding: 0 }`.
* **Lexicographical Timestamp Inversion (L57, L126)**: Sorting via `a.entry_timestamp_utc < b.entry_timestamp_utc` places `'2026-10-10T10:00:00.500Z'` *before* `'2026-10-10T10:00:00Z'` because ASCII `'.'` (`0x2E`) < `'Z'` (`0x5A`), reversing chronological order when fractional-second and whole-second ISO timestamps are mixed. Entry timestamps are also never validated via `validateIso8601UtcTimestamp` or checked against `entry_timestamp_utc >= position_inception_utc` (allowing negative `lifecycle_recovery_duration_days`).
* **Missing Two-Tier Clearing Model & Incomplete Double-Counting Check (L24–L40)**: `cashFlowEngine.ts` does not track Tier 1 clearing (`B_clearing`) vs Tier 2 bank liquidity (`B_bank`/`L_bank`), and `validateCashFlowDoubleCounting` permits combining `GROSS_CHECKOUT_PROCEEDS` with `NET_MERCHANT_PROCEEDS`.
* **Transient Breakeven Misclassification (L165–L199)**: `computePostOutlayRecoveryMetrics` reports `status: 'RECOVERED'` at the first $k > k_{\text{outlay}}$ with $B_{\text{ops}}(k) \ge 0$, even if subsequent operating outflows leave $B_{\text{ops}}(K) < 0$.
* **PO Lifecycle Corruption (L270–L319)**: `CommittedCapitalManager.fulfillPO('PO-1', -50000)` on a `100000` PO sets `relief = Math.min(-50000, 100000) = -50000`, increasing `unfulfilled_commitment` and `total_committed_capital` to `150000`. Moreover, `cancelPO` and `replacePO` do not reject `'FULFILLED'` POs, and `amendPO` (`PO_AMENDED`, Spec §7.2 `AUDIT-18`) is missing.
* **Missing XIRR / Return Solver**: The polynomial NPV / XIRR solver required by Charter §2.2 and Spec §7.2 is absent.


* **Consequence**: Miscomputed peak funding, inverted intraday sequences, corrupted committed-capital limits, and absent return solver capabilities.
* **Recommended Remediation**: Represent cash-flow amounts in `CanonicalMoney` (`bigint` subunits with verified single `CurrencyCode`), validate all timestamps with `validateIso8601UtcTimestamp`, sort by `(Date.parse(entry_timestamp_utc), sequence_number)`, reject pre-inception timestamps, implement the Two-Tier Gross-Clearing ledger (`B_clearing` and `B_bank`), validate positive safe integers and terminal states in `CommittedCapitalManager` (adding `amendPO`), and implement the Charter §2.2 XIRR solver.
* **Regression Test / Closure Criterion**: Execute all Spec §8.1–§8.2 financial tests (`FIN-GROSS-CLEARING-TIER-037`, `FIN-ROPF-PEAK-007`, `FIN-CONV-HPR-008`, `FIN-PO-NETTING-003` with cancellation + fulfillment + amendment) plus negative tests for `NaN`, mixed `.000Z`/`Z` timestamps, and negative PO fulfillment.
* **Verification Status**: Independently verified via static analysis and Node.js execution (`verify_counterexamples.mjs`).


6. **`ARGON-PERSIST-001` — WAL Blank-Line Byte Undercount on Torn-Tail Truncation, Pre-Integrity Disk Mutation, Boundary 3 Double-Counting & Poisoned Recovery Portfolio Mutation**
* **Severity / Confidence**: High / High
* **Category & Affected Gate**: Persistence, Concurrency & Crash Recovery (Gate M3 & WAL Addendum `POC-001-M3-ADDENDUM-001`)
* **Location**: `Market-HFT-OS` (`a1bd359`), `src/persistence/durableRecoveryJournal.ts` (`FileBackedDurableRecoveryJournal`, L205–L280; `CrashRecoveryEngine.recover`, L470–L524; `CrashRecoveryEngine.recoverDurable`, L535–L638)
* **Violated Requirement**: Gate M3 WAL Durability & Exact-Once Crash Recovery Invariants.
* **Failure Mechanism & Minimal Counterexamples**:
* **Blank-Line / CRLF Byte Undercount (L220–L253)**: In `FileBackedDurableRecoveryJournal` constructor, `if (line.trim().length === 0) continue;` skips adding the bytes of any blank line (`\n` = 1 byte, `\r\n` = 2 bytes) to `validBytesLength`. If a WAL contains a blank line before a torn tail, `fs.ftruncateSync(fd, validBytesLength)` truncates into the last valid record on disk.
* **Disk Truncation Before Hash-Chain Verification (L249–L266)**: `fs.ftruncateSync` mutates the WAL file at L253 *before* `super(initialEntries)` calls `verifyIntegrity()` at L63. Conversely, if a torn tail happens to be valid JSON syntax (`JSON.parse` succeeds) but has a truncated/corrupted `entry_sha256`, `tornTailPolicy: 'TRUNCATE_TORN_TAIL'` does not catch it and fails closed at `super(initialEntries)`.
* **Boundary 3 Double-Counting & Out-of-Order Execution (L575–L628)**: In `CrashRecoveryEngine.recoverDurable`, a Boundary 3 fill (`PORTFOLIO_APPLIED` present in WAL, fill not yet in `portfolio`) is processed in the first loop (`L585`: `portfolio.processFill`, `recoveredCount++`) and then visited again in the second loop (`L593`: `isProcessedInPortfolio` is now `true` and `isAppliedInJournal` is `true`, so `skippedDuplicateCount++` executes at `L614`). A single recovered fill increments both `recovered_fills_count` (`1`) and `skipped_duplicate_fills_count` (`1`), and Boundary 3 fills execute before earlier Boundary 1 fills, which can fail with `E-ERR-042: INSUFFICIENT_INVENTORY`.
* **Poisoned Journal Mutates Portfolio Before Failing (L272–L279, L619–L622)**: Constructor normalization failure swallows the exception and leaves `isPoisoned = true`. Calling `recoverDurable` mutates `portfolio` in memory at L619 before `journal.appendEvent` throws `E-ERR-024: JOURNAL_POISONED` at L622.


* **Consequence**: Disk WAL corruption on torn-tail recovery after blank lines, corrupted recovery metrics, out-of-order fill replay failures, and in-memory portfolio divergence on poisoned journals.
* **Recommended Remediation**: Track exact byte offsets directly from `fileBuffer` slices; validate hash-chain continuity per line during the scan so corrupt final JSON lines are recognized as torn tails while corrupt interior lines abort before `ftruncateSync`; check `if (journal instanceof FileBackedDurableRecoveryJournal && journal.getIsPoisoned()) throw ...` at the top of `recoverDurable`; and unify Boundary 1/2/3 handling into a single chronological pass over `recordedFills`.
* **Regression Test / Closure Criterion**: Add tests for blank-line + torn-tail truncation, Boundary 1 BUY followed by Boundary 3 SELL, and `recoverDurable` on a poisoned journal asserting atomic portfolio invariance.
* **Verification Status**: Independently verified via static analysis and Node.js execution (`verify_counterexamples.mjs`).


7. **`ARGON-SIM-001` — Infinite Offer Quantity Replay, Same-Millisecond `intent_id` Collision, Fabricated Supplier Intent Hash, Truncated WACB & Untyped Crash Worker**
* **Severity / Confidence**: High / High
* **Category & Affected Gate**: Simulation Execution, Portfolio Accounting & Reproducibility (Gate M2 / Gate M3)
* **Location**: `Market-HFT-OS` (`a1bd359`), `src/simulation/simulationPipeline.ts` (L108–L113, L125–L218, L259–L285), `src/execution/engine.ts` (L73), `src/execution/simulatedGateway.ts` (L106–L202), `src/portfolio/simulationPortfolio.ts` (L196–L216, L264, L348–L393), `scripts/test_crash_worker.ts` (L25–L79)
* **Violated Requirement**: Gate M1 Spec §2.1, Gate M2/M3 Quantity Conservation, Idempotency & Deterministic Digest Invariants.
* **Failure Mechanism & Minimal Counterexamples**:
* **Infinite Offer Replay (`simulationPipeline.ts` L138–L215)**: `verifiedOffers` never decrements `offer.available_quantity` after a fill; a 100-unit supplier offer is re-bought and re-sold on every subsequent market tick without bound.
* **Same-Millisecond Tick Collision (`engine.ts` L73)**: `intentId = intent:dryrun:${offer.offer_id}:${Date.parse(evaluated_at_utc)}` collides whenever two ticks share the same millisecond timestamp (or when `MonotonicVirtualClock` uses its default `autoAdvanceStepMs = 0`), causing `SimulatedExecutionGateway.submitExecutionIntent` to throw `E-ERR-039` or `simulateFill` to throw `E-ERR-036`.
* **Fabricated Supplier Intent Hash (`simulationPipeline.ts` L180, `simulatedGateway.ts` L106)**: `supplierIntent.canonical_intent_sha256` is set to `sha256(Buffer.from('sup:' + intent.canonical_intent_sha256))` rather than `sha256(canonicalizeJCS(supplierIntent.payload))`, and `SimulatedExecutionGateway` never verifies `intent.canonical_intent_sha256`.
* **Missing `offer_status` Check (`simulationPipeline.ts` L109)**: `registerVerifiedOffer` checks `verification_status !== 'VERIFIED'` but not `offer_status === 'VERIFIED_EXECUTABLE_OFFER'`.
* **Incomplete State Digest (`simulationPipeline.ts` L259–L285)**: `computeStateDigest()` hashes only `.length`/`.size` counts for events, offers, step reports, and portfolio journal entries, omitting all gateway orders, transition events, and journal payloads.
* **Floor Truncation of WACB & Unvalidated Checkpoints (`simulationPortfolio.ts` L264, L348–L393)**: `weighted_cost_basis_subunits` uses `aggCostBig / BigInt(netQty)` (floor truncation) instead of `divideHalfEven`, and `restoreFromCheckpoint` does not verify capital conservation (`available_cash + sum(aggregate_cost) === initial_cash + cumulative_realized_pnl`) or epoch quantity invariants (`epoch_start_quantity - epoch_cumulative_sold_quantity === net_quantity`).
* **Untyped Crash Worker (`scripts/test_crash_worker.ts` L25–L79)**: Uses non-existent fields (`timestamp_utc`, `requested_quantity`, `limit_price`) that fail TypeScript compilation if `scripts/` is included in `tsconfig.json`.


* **Consequence**: Economically invalid multi-tick simulations, crashes on same-millisecond ticks, undetected journal tampering in pipeline digests, and schema drift in crash workers.
* **Recommended Remediation**: Track remaining offer quantity in `SimulationPipeline` (transitioning exhausted offers out of executable status); include `feed.event_id` or a monotonic counter in `intentId`; compute and verify true JCS SHA-256 digests on all `ExecutionIntent` instances; enforce `offer.offer_status === 'VERIFIED_EXECUTABLE_OFFER'` in `registerVerifiedOffer`; use `divideHalfEven` for `weighted_cost_basis_subunits`; validate conservation laws in `restoreFromCheckpoint`; include full journals/orders in `computeStateDigest()`; and add `"scripts/**/*"` to `tsconfig.json`.
* **Regression Test / Closure Criterion**: Multi-tick offer exhaustion test, same-millisecond tick test, corrupted-checkpoint rejection test, and `tsc --noEmit` covering `scripts/`.
* **Verification Status**: Independently verified via static analysis.


8. **`ARGON-SEC-001` — PAT Environment Variable Exposure (`GIT_PAT_SECRET`), Unreviewed 3-Second `git add -A` Daemon & Secret Exclusion Mismatch**
* **Severity / Confidence**: High / High
* **Category & Affected Gate**: Security, DevSecOps & Repository Governance (Gate M0 / Gate M3)
* **Location**: `Market-HFT-OS` (`a1bd359`), `scripts/sync_repos.py` (L30–L37, L63–L79, L130–L165), `scripts/git_askpass.py` (L20–L31), `.gitignore` (L1–L30), `ADRs/.gitignore` (L1–L16)
* **Violated Requirement**: Project Charter §8 (`DEC-017`) & Section 3/6.F Security Controls.
* **Failure Mechanism**:
* `sync_repos.py` L70 injects `env["GIT_PAT_SECRET"] = token` into the environment of every `git` command (`status`, `rev-parse`, `log`, `add`, `reset`, `commit`, `push`, `fetch`), exposing the raw GitHub PAT to any child process, git hook, or crash dump.
* `sync_repos.py` L132 runs `git add -A` every 3 seconds in daemon mode and pushes `HEAD:refs/heads/main` without human review, branch verification, or file-size limits.
* `FORBIDDEN_FILES` in `sync_repos.py` L30–L37 resets `Alpaca_Key.env` and `Eulerpool.env`, whereas `Market-HFT-OS/.gitignore` lists `Alpaca_Key.txt` and `Eulerpool.txt`, and `ADRs/.gitignore` omits `Eulerpool.txt` and `Alpaca_Key.txt` entirely.


* **Consequence**: Accidental secret leakage into Git history or subprocess environments and unreviewed automated commits to `main`.
* **Recommended Remediation**: Remove `GIT_PAT_SECRET` from `sync_repos.py` (let `git_askpass.py` read the token file directly only when invoked by `git push`/`git fetch`, and only attach `GIT_ASKPASS` on remote network operations); remove automatic `git add -A` commits; and synchronize `FORBIDDEN_FILES` and `.gitignore` across both repositories.
* **Regression Test / Closure Criterion**: Static security test verifying `GIT_PAT_SECRET` is absent from subprocess environments and `.gitignore` / `FORBIDDEN_FILES` match across repos.
* **Verification Status**: Independently verified via static code review.


9. **`ARGON-SEC-002` — Unbounded `pendingGapBuffer` Memory Growth, Synchronous $O(\Delta\text{seq})$ Replay Loop Freeze & Missing Feed Quantity/Sequence Validation**
* **Severity / Confidence**: Medium / High
* **Category & Affected Gate**: Application Security & Feed Resilience (Gate M2 / Gate M3)
* **Location**: `Market-HFT-OS` (`a1bd359`), `src/feeds/feedHandler.ts` (L160–L203), `src/feeds/localWebSocketTransport.ts` (L224–L237), `src/feeds/streamingAdapter.ts` (L137–L147)
* **Violated Requirement**: Bounded resource consumption and fail-closed input validation at ingestion boundaries.
* **Failure Mechanism**:
* `MarketFeedHandler.pendingGapBuffer` (L178–L183) has no size cap or eviction when a sequence gap is unrecoverable.
* `MockLocalWebSocketFeedServer.handleClientMessage` (L229) and `SimulatedStreamingMarketFeedAdapter.recoverGapViaReplay` (L141) execute `for (let seq = fromSeq; seq <= toSeq; seq++)` without bounding `toSeq - fromSeq`; a single frame with `sequence: "1000000000"` locks the Node.js event loop for $10^9$ iterations.
* `ingestRawMessage` (L160) calls `BigInt(raw.sequence)` before validating format via `parseCanonicalStreamSequence`, throwing an unhandled exception on malformed strings instead of returning `INVALID_FORMAT`, and never validates `bid_quantity`, `ask_quantity`, or positive/uncrossed prices.


* **Consequence**: Memory exhaustion (OOM) or 100% CPU freeze from a single malformed or high-sequence WebSocket tick.
* **Recommended Remediation**: Enforce `parseCanonicalStreamSequence(String(raw.sequence))`, positive safe-integer quantity checks, and positive price checks in `ingestRawMessage` (returning `INVALID_FORMAT` on failure); cap `pendingGapBuffer` at `maxReplayBufferSize`; and reject replay requests where `toSeq < fromSeq` or `toSeq - fromSeq > BigInt(maxReplayBufferSize)`.
* **Regression Test / Closure Criterion**: Adversarial feed tests with `sequence: "1000000000"`, `sequence: "abc"`, `sequence: "-1"`, and `bid_quantity: -10`.
* **Verification Status**: Independently verified via static code review.


10. **`ARGON-PERSIST-002` — Missing Offer-Stream Hash Chaining ($H_{n-1}$), DDL Drift vs Spec §4.1, Incomplete JCS Input Domain Checks & One-Way Actuals Guard**
* **Severity / Confidence**: Medium / High
* **Category & Affected Gate**: Persistence, Serialization & Dual-Ledger Isolation (Gate M1)
* **Location**: `Market-HFT-OS` (`a1bd359`), `src/persistence/atomicPromotion.ts` (L284–L316), `src/persistence/postgresAdapter.ts` (L17–L62, L114–L178), `src/canonical/jcs.ts` (L10–L15), `src/ledger/actualsGuard.ts` (L83–L173)
* **Violated Requirement**: Gate M1 Spec §1 Invariant 15, §2.3 (`SIM-GUARD-002`, `ActualsAuthTicketPayload.expires_at_utc`), §4.1, §5.1, §6.1 (`AUDIT-32`).
* **Failure Mechanism**:
* `OfferPromotionEventPayload` and `offer_stream_events` omit `previous_event_hash` ($H_{n-1}$), so offer stream events are not hash-chained ($H_n = \text{SHA-256}(H_{n-1} \parallel \text{canonicalizeJCS}(e_n))$).
* `POSTGRES_SCHEMA_DDL` in `postgresAdapter.ts` differs from Spec §4.1 (`offer_id` vs `stream_id` PK in `offer_stream_heads`, `JSONB` vs `TEXT`, `BYTEA` vs `TEXT`) and uses `NOW()` instead of `tx_auth_time_utc`.
* `src/canonical/jcs.ts` does not check for lone UTF-16 surrogates (`E-ERR-022`), throws a generic error from `json-canonicalize` instead of `E-ERR-022` on non-finite numbers, and lacks a duplicate-key-rejecting JSON parser (`JCS-EDGE-002`).
* `src/ledger/actualsGuard.ts` implements `enforceActualsLedgerWrite` (`E-ERR-020`) but omits `enforceSimulationLedgerWrite` (`E-ERR-025: SIMULATION_LEDGER_WRITE_VIOLATION`, required by `SIM-GUARD-002`) and does not check `exp_ms - iss_ms === 300000` on `ActualsAuthTicketPayload` (required by Spec §2.3 L519).


* **Consequence**: Offer stream events can be deleted/reordered at the database layer without breaking a hash chain; JCS boundary errors and reverse dual-ledger violations are not caught as specified.
* **Recommended Remediation**: Add `previous_event_hash` to `offer_stream_heads` and `offer_stream_events`; pass `tx_auth_time_utc` to all SQL inserts; add lone-surrogate, `E-ERR-022`, and duplicate-key checks in `src/canonical/jcs.ts`; and add `enforceSimulationLedgerWrite` (`E-ERR-025`) and exact 300s ticket lifetime validation in `src/ledger/actualsGuard.ts`.
* **Regression Test / Closure Criterion**: Execute `JCS-EDGE-002`, `JCS-STRICT-DOMAIN-003`, `STREAM-ERR-002`, and `SUITE-06` (`ACTUALS-GUARD-001` through `TEST-CONCURRENCY-NONCE-01`).
* **Verification Status**: Independently verified via static code review.



#### 3.2 Specification, Governance & Verification Conflicts

11. **`ARGON-SPEC-001` — Internal Contradictions & Embedded Code Bugs in Frozen Gate M1 Specification v1.13 Final**: As detailed in `DISC-03` and `ARGON-REVIEW-NOTE-ADRS.md`, `ADRs/POC-001_Gate_M1_Design_Readiness_Specification.md` contains three internal defects in its embedded TypeScript reference code: (§3.2 vs §3.3) conflicting `claim_signing_payload_sha256` vs `claim_payload_digest` (`params_sha256`), (§3.2 L1038–L1046) nested `if (principal.compromised)` inside `if (principal.revoked)` in `validateAttesterAuthority`, and (§2.1 L225–L240) unverified self-asserted `oracle_public_key_hex` in `validateFXReceiptAtPointOfUse`. (**Severity: High / Confidence: High**)
12. **`ARGON-GOV-001` — Internal Self-Contradiction in Gate M3 Conformance Report (`POC-001-M3-CONF-001`)**: Sections 1–3 report commit `7415c61` with 123 passed / 3 skipped tests and Suite 17 `OPEN (CONDITIONALLY GATED)`, while Sections 4.4–5 of the same file report commit `a1bd359 (unpushed)` with 129 passed / 0 skipped tests and Suite 17 `6/6 PASS`. (**Severity: High / Confidence: High**)
13. **`ARGON-GOV-002` — Unreconciled Charter/Spec Status Headers & Cross-Repo Spec Hash Divergence**: `PROJECT_CHARTER.md` v0.2.4 and `POC-001_Gate_M1_Design_Readiness_Specification.md` v1.13 still carry pre-approval `PROPOSED` / `BLOCKED` headers, and the copy of the M1 Spec in `Market-HFT-OS/AG/` has a different SHA-256/blob hash (`c52fe522...` / `6a95577a...`) than the authoritative copy in `ADRs/` (`efaa93d8...` / `ac8899da...`). (**Severity: High / Confidence: High**)
14. **`ARGON-GOV-003` & `ARGON-TEST-001` — Overstated Conformance Matrix & 73 Missing Specified Test Cases**: 73 of 111 test IDs in Gate M1 Spec §8.1–§8.2 are missing from `tests/`; 7 exported functions (`normalizeProductIdentityCore`, `generateCanonicalProductId`, `createPhysicalDimensions`, `validateInventoryQuantity`, `computeRoPF`, `computeCoC`, `computeHPR`) and the entire `GATEWAY_CLAIM_ENDORSEMENT` promotion path have 0 test calls; `suite09` and `suite11` test local test-file functions rather than production exports; and `Market-HFT-OS/README.md` is stale (116 vs 129 tests). (**Severity: High / Confidence: High**)
15. **`ARGON-GOV-004` — Misclassified Research Corpus `.docx` Files in `ADRs`, Missing `DOC-001`, UTF-16LE Log Artifact & `.gitignore` Drift**: `ADRs` contains `002.docx`–`009.docx` (research corpus documents `DOC-002`–`DOC-009`, missing `DOC-001`), `POC-001_Gate_M3_Typecheck_Execution_Results.txt` is UTF-16LE encoded, and `ADRs/.gitignore` omits `Eulerpool.txt` and `Alpaca_Key.txt`. (**Severity: Medium / Confidence: High**)
16. **`ARGON-UX-001` — Absence of Operator UI/CLI Surface & Proposed Information Architecture (Workstream H)**:
* **Severity / Confidence**: Informational / High
* **Finding**: Inspection of `Market-HFT-OS` confirms that **no user interface, operator dashboard, web frontend, or interactive CLI exists** in the repository (`src/` contains only backend TypeScript library modules and `scripts/` contains only git sync helpers and a test worker). No visual behavior was tested because none exists.
* **Proposed Operator Surface & Safety Information Architecture (Wireframe-Level Recommendation Only — Do Not Add UI Dependencies Without Owner Approval)**:
When an operator surface is eventually authorized (recommended initially as a zero-dependency read-only terminal/HTML diagnostic report before any interactive framework is considered), it must enforce five visual and operational guardrails:
1. **Persistent Mode & Kill-Switch Banner (Top Global Header)**: Always-visible top bar displaying current operating mode (`SIMULATION / PAPER ONLY — LIVE EXECUTION DISABLED`), WAL health status (`HEALTHY` vs `POISONED — FAIL CLOSED`), and a single-action **Emergency Halt / Kill Switch** (`PROJECT_CHARTER.md` §5.2) that halts feed ingestion and intent generation immediately without requiring nested menus.
2. **Strict Dual-Ledger Split View (`PROJECT_CHARTER.md` §3.3, `DEC-016`)**: Physically separate panels (with distinct semantic styling and labels) for **Paper Simulation Ledger** (`SIMULATION_LEDGER`) vs **Real-World Actuals Ledger** (`ACTUALS_LEDGER` — read-only bank/settlement reconciliation), displaying the **Real vs. Paper Money Ratio** and slippage/friction delta.
3. **4D Evidence Provenance & Epistemic Badges**: Every displayed price, fee, or return metric must carry an inline badge showing all four dimensions (`Evidence Kind | Verification Status | Offer Status | Source Freshness Age`), visually distinguishing `OBSERVED / VERIFIED` facts from `SCENARIO / FORECAST / SYNTHETIC_TEST` assumptions so forecasts can never be mistaken for facts.
4. **Explicit `DATA REQUIRED` / `NOT YET RECOVERED` States**: Unvalidated tax schedules, inflation deflators, unverified inventory valuations, or open unrecovered positions must render explicit `DATA REQUIRED` or `NOT YET RECOVERED` badges — never `0.00%` or `0 days`.
5. **Two-Tier Liquidity & Capital Exposure Panel**: Display Tier 1 Encumbered Marketplace Clearing (`B_clearing`), Tier 2 Deployable Bank Cash (`B_bank`/`L_bank`), Committed PO Capital (`C_committed`), Intraday Peak Operating Funding (`C_peak,ops`), and Inventory Bucket states (`IN_TRANSIT`, `AVAILABLE`, `RESERVED`, `DAMAGED`).





### Output 4 — Cross-Repository Conformance Matrix

| Requirement / Source | Implementation Location (`Market-HFT-OS`) | Test / Evidence Reference | Current Verification Status | Gap or Contradiction | Required Action |
| --- | --- | --- | --- | --- | --- |
| **Gate M0 Quarantine Isolation** (`Charter §8, DEC-001; Spec §1 Inv. 1`) | `.gitignore` (`/_salvage/`), `src/` (0 imports) | `suite08_quarantine_isolation.test.ts` (`QUARANTINE-IMPORT-BAN-002`, `QUARANTINE-READONLY-001`) | **DESIGN REVIEWED** | `suite08` scans `src/` but omits `tests/` and `scripts/`; `_salvage/` not present in archive. | Extend `suite08` to scan `tests/` and `scripts/`. |
| **RFC 8785 JCS & Package Provenance** (`Spec §6.1, AUDIT-22, 32, 45`) | `src/canonical/jcs.ts`, `package.json`, `package-lock.json` | `suite01_serialization.test.ts` (6 tests: `KAT-01`, `KAT-02`, `NaN`/`Infinity`) | **CONFLICT** | Missing 6 pinned `cyberphone` fixtures (`JCS-CONF-PINNED-001`), missing duplicate-key parser (`JCS-EDGE-002`), missing lone-surrogate check & `E-ERR-022` error code (`ARGON-PERSIST-002`). | Add lone-surrogate/error-code wrapper, duplicate-key parser, and 6 pinned `cyberphone` fixture tests. |
| **3-Tier Currency Registry & `CanonicalMoney**` (`Spec §2.1, AUDIT-10`) | `src/canonical/domain.ts` (`CURRENCY_REGISTRY`, `createCanonicalMoney`) | `suite02_currency.test.ts` (`CURR-REG-3SCALE-LOOKUP-001`, `CURR-SCALE-001`, `CURR-BOUND-001`) | **DESIGN REVIEWED** | `SimulationPortfolio` and `convertMoneySubunitsExact` do not call `createCanonicalMoney` on input money objects. | Enforce `createCanonicalMoney` at all module entry points. |
| **Cross-Currency Addition Prohibition & Point-of-Use FX Receipts** (`Spec §2.1, AUDIT-11`) | `src/canonical/currency.ts` (`convertMoneySubunitsExact`, `validateFXReceiptAtPointOfUse`) | `suite02_currency.test.ts` (`KAT-04A/B`), `suite11_cross_currency.test.ts` | **CONFLICT** | `validateFXReceiptAtPointOfUse` trusts self-asserted `oracle_public_key_hex`; `convertMoneySubunitsExact` misparses `rateDecimal` when fractional digits $\ne$ `rateScale` (`ARGON-FIN-001`); `suite11` tests a local helper `sumMoneyDirect` inside the test file. | Authenticate oracle keys against registry, validate `rateDecimal` scale/positivity, and export production `addCanonicalMoney` guard. |
| **Product Identity Normalization & Volumetric Weight** (`Spec §2.2, AUDIT-17, 25, 33, 40`) | `src/canonical/product.ts` (`normalizeProductIdentityCore`, `calculateVolumetricWeightGrams`, `validateInventoryQuantity`) | `suite07_financial_engine.test.ts` (`VOL-SAFEINT-001`, `VOL-BOUND-002`, `VOL-ROUND-HALFUP-003`) | **SPECIFIED — PENDING VERIFICATION** | `calculateVolumetricWeightGrams` is tested, but `normalizeProductIdentityCore`, `generateCanonicalProductId`, `createPhysicalDimensions`, and `validateInventoryQuantity` have **0 test calls** (`PROD-NORM-*`, `INV-QTY-BOUND-002` missing). | Add unit tests for all 4 untested functions in `src/canonical/product.ts`. |
| **18-Tuple Fail-Closed Evidence Allowlist & Document Correspondence** (`Charter §3.1, DEC-013; Spec §3.1, AUDIT-01, 07`) | `src/canonical/allowlist.ts` (`validateEvidenceAllowlistEligibility`) | `suite04_historical_exclusion.test.ts` (`ALLOW-FAIL-001`) | **CONFLICT** | `validateEvidenceAllowlistEligibility` is never called by `gate.ts` or `atomicPromotion.ts`, and `ResolvedEvidenceEnvelope` lacks 4D attributes (`ARGON-EVID-001`). | Wire `validateEvidenceAllowlistEligibility` into `gate.ts` and `atomicPromotion.ts` and populate 4D fields on `ResolvedEvidenceEnvelope`. |
| **Four-Claim Promotion Gate, Attester Authority & Gateway Receipts** (`Spec §3.2–§3.3, AUDIT-02..09, 12..14, 24, 26..28, 31, 35, 41, 46, 47`) | `src/verification/claims.ts`, `src/verification/gate.ts`, `src/persistence/atomicPromotion.ts` | `suite03_promotion_gate.test.ts`, `suite04`, `suite05`, `suite06` | **CONFLICT** | (1) `validateAttesterAuthority` fails open on `{revoked:false, compromised:true}` and `{revoked:true}` without `revoked_at_utc` (`ARGON-CRYPTO-002`). (2) Gateway receipt digest check in `atomicPromotion.ts` is tautological and `gate.ts` accepts `params_sha256` without `offer_id` or `operator_id` binding (`ARGON-CRYPTO-001`). (3) `GATEWAY_CLAIM_ENDORSEMENT` has 0 end-to-end promotion tests. | Fix `validateAttesterAuthority`, require full `ClaimSigningPayload` digest and `operator_id`/`operator_role` matching on gateway receipts, and add gateway promotion tests. |
| **PostgreSQL Row-Locked Atomic Promotion & Ambiguous Commit Reconciliation** (`Spec §4.1, AUDIT-21, 23, 29, 30, 36, 37, 39, 42, 43, 49, 51`) | `src/persistence/atomicPromotion.ts`, `src/persistence/postgresAdapter.ts` | `suite03`, `suite12_durable_persistence.test.ts`, `suite16`, `suite17` (gated on `DATABASE_URL`) | **CONFLICT** | Row-lock protocol and 6-path reconciliation logic are implemented, but post-lock gateway digest revalidation (`AUDIT-47`) is tautological (`ARGON-CRYPTO-001`), DDL in `postgresAdapter.ts` diverges from Spec §4.1, and `NOW()` is used instead of `tx_auth_time_utc` (`ARGON-PERSIST-002`). | Fix post-lock digest revalidation, reconcile SQL DDL with Spec §4.1, and pass `tx_auth_time_utc` into SQL queries. |
| **Hash-Chained Event Streams & Checkpoint Trust Anchoring** (`Spec §5.1–§5.2, AUDIT-15, 19`) | `src/checkpoint/trustAnchor.ts`, `src/persistence/atomicPromotion.ts`, `src/persistence/durableRecoveryJournal.ts` | `suite09_virtual_genesis.test.ts`, `suite10_checkpoint_anchor.test.ts` | **CONFLICT** | `verifyStreamCheckpointReceipt` is implemented, and `DurableRecoveryJournal` hashes `prev_entry_sha256`, but `OfferPromotionEventPayload` / `offer_stream_events` omit `previous_event_hash` ($H_{n-1}$), and `suite09` tests a hardcoded local object inside the test file (`ARGON-PERSIST-002`, `ARGON-TEST-001`). | Add `previous_event_hash` chaining to `offer_stream_events` and rewrite `suite09` to test production stream code. |
| **Two-Tier Gross-Clearing Accounting, Peak Funding, Recovery Timelines, PO Netting & XIRR Solver** (`Charter §2.2, DEC-012, 014; Spec §7.1–§7.3, AUDIT-16, 18, 34, 38, 44, 48, 50`) | `src/financial/cashFlowEngine.ts` | `suite02` (`FIN-PEAK-INDEPENDENT-EQUITY-041`), `suite07_financial_engine.test.ts` | **CONFLICT** | Uses float `number` instead of `CanonicalMoney`/`bigint`; fails open on `NaN`; lexicographical timestamp sort inverts `.500Z` vs `Z`; Two-Tier Clearing (`B_clearing`/`B_bank`), `PO_AMENDED`, and XIRR solver are **NOT IMPLEMENTED**; `computeRoPF`, `computeCoC`, and `computeHPR` have 0 test calls (`ARGON-FIN-002`). | Refactor `cashFlowEngine.ts` to `CanonicalMoney`/`bigint`, implement Two-Tier Clearing, `amendPO`, and XIRR solver, fix timestamp sorting, and add full test coverage. |
| **Bidirectional Dual-Ledger Isolation Guard** (`Charter §3.3; Spec §2.3, AUDIT-20, SUITE-06`) | `src/ledger/actualsGuard.ts` (`enforceActualsLedgerWrite`) | `suite13` (`M2-EXEC-DUAL-LEDGER-GUARD-013`) | **CONFLICT** | Reverse guard `E-ERR-025: SIMULATION_LEDGER_WRITE_VIOLATION` (`SIM-GUARD-002`) is **NOT IMPLEMENTED**; lines 93–173 of `actualsGuard.ts` (ticket, role, digest, signature, and nonce checks) have **0% test coverage** (`SUITE-06` from Spec §8.1 was omitted). | Implement `enforceSimulationLedgerWrite` (`E-ERR-025`), enforce 300s ticket lifetime, and implement all 6 `SUITE-06` tests. |
| **Market Feed Normalization, Loopback WebSocket Transport & Simulated Execution Gateway** (`Gate M2 Report §2.1–§2.3`) | `src/feeds/feedHandler.ts`, `src/feeds/streamingAdapter.ts`, `src/feeds/localWebSocketTransport.ts`, `src/execution/engine.ts`, `src/execution/simulatedGateway.ts` | `suite13_market_feed_execution.test.ts`, `suite14_websocket_portfolio.test.ts`, `suite15` | **CONFLICT** | Unbounded `pendingGapBuffer` and unbounded `for (seq = fromSeq; seq <= toSeq)` replay loop (`ARGON-SEC-002`); same-millisecond `intent_id` collision and unverified `canonical_intent_sha256` (`ARGON-SIM-001`). | Bound `pendingGapBuffer` and replay request ranges, validate feed quantities/sequences, and disambiguate `intent_id`. |
| **Simulation Portfolio Cumulative COGS & End-to-End Pipeline** (`Gate M2 Report §2.4, §4`) | `src/portfolio/simulationPortfolio.ts`, `src/simulation/simulationPipeline.ts` | `suite14`, `suite15_e2e_simulation_pipeline.test.ts` | **CONFLICT** | Single-epoch cumulative COGS $A(s) = \operatorname{divideHalfEven}(C_0 \cdot s, Q_0)$ is mathematically sound, but `SimulationPipeline` never decrements `offer.available_quantity` (infinite inventory replay), fabricates `supplierIntent` hash, truncates WACB, and omits journals/orders from `computeStateDigest()` (`ARGON-SIM-001`). | Decrement offer available quantity on fills, fix `supplierIntent` JCS hash, use `divideHalfEven` for WACB, and include full state in `computeStateDigest()`. |
| **File-Backed WAL Durability, Boundary Normalization & Crash Recovery** (`Gate M3 Report & Addendum POC-001-M3-ADDENDUM-001`) | `src/persistence/durableRecoveryJournal.ts`, `scripts/test_crash_worker.ts` | `suite16_crash_recovery_persistence.test.ts` | **CONFLICT** | Blank lines before torn tails undercount `validBytesLength` and truncate valid records; `ftruncateSync` runs before `verifyIntegrity()`; Boundary 3 double-counts fills and executes out of order; poisoned journal mutates `portfolio` before throwing (`ARGON-PERSIST-001`). | Fix byte-offset accounting, check integrity before truncation, unify recovery into one chronological loop, and check `getIsPoisoned()` before mutating `portfolio`. |
| **Token Security & Repository Synchronization** (`Charter §8, DEC-017; Gate M3 Report §4.3`) | `scripts/sync_repos.py`, `scripts/git_askpass.py`, `.gitignore` | Static inspection (`sync_repos.py`, `git_askpass.py`) | **CONFLICT** | `sync_repos.py` injects `GIT_PAT_SECRET` into all `git` subprocess environments, runs unreviewed `git add -A` every 3s, and mismatches `FORBIDDEN_FILES` vs `.gitignore` (`ARGON-SEC-001`). | Remove `GIT_PAT_SECRET` env injection, disable unreviewed `git add -A`, and align secret ignore lists. |

### Output 5 — Adversarial Test Plan

| Test ID | Target Module & Category | Adversarial Input / Fault Scenario | Current (Defective) Behavior | Required Pass Criterion |
| --- | --- | --- | --- | --- |
| **ADV-CRYPTO-01** | `atomicPromotion.ts` / `gate.ts` (Cryptographic Gate) | Submit `GATEWAY_CLAIM_ENDORSEMENT` claim where `rcpt.claim_signing_payload_sha256` is signed over Offer A (`off:A`), attached to Offer B (`off:B`), or where `rcpt.operator_id !== claim.attestation.attester_id`. | `atomicPromotion.ts` L254 tautologically passes when `claim_payload_digest` is omitted; `gate.ts` passes if `claim_payload_digest === params_sha256`; operator mismatch ignored. | Rejects fail-closed with `E-ERR-017` in both Phase 1 (`gate.ts`) and Phase 2 (`atomicPromotion.ts`); 0 nonces consumed. |
| **ADV-CRYPTO-02** | `claims.ts` (`validateAttesterAuthority`) | Authenticate claim with principal `{ revoked: false, compromised: true }` or `{ revoked: true, revoked_at_utc: undefined }`. | Returns principal as valid (`ACCEPTED`). | Throws `E-ERR-019: OPERATOR_KEY_REVOKED` fail-closed in both cases. |
| **ADV-FIN-01** | `currency.ts` (`convertMoneySubunitsExact` & `validateFXReceiptAtPointOfUse`) | (a) Convert `'10000'` USD subunits (`$1.0000`) to INR with `rateDecimal = "86.5"`, `rateScale = 6`.<br>

<br>(b) Sign an `FXConversionReceipt` (`exchange_rate: "999999.000000"`) using a freshly generated attacker Ed25519 keypair. | (a) Returns `'9'` subunits (`₹0.0009`) instead of `'865000'` (`₹86.5000`).<br>

<br>(b) `validateFXReceiptAtPointOfUse` accepts the attacker's self-asserted key. | (a) Rejects mismatched fractional scale or normalizes exact decimal position to `'865000'`.<br>

<br>(b) Rejects unregistered/untrusted oracle public key with `E-ERR-008`. |
| **ADV-FIN-02** | `cashFlowEngine.ts` (Sorting, Boundary & Metamorphic) | (a) Pass `[{ entry_timestamp_utc: '2026-10-10T10:00:00Z', sequence_number: 1, amount: -1000 }, { entry_timestamp_utc: '2026-10-10T10:00:00.500Z', sequence_number: 2, amount: 1000 }]`.<br>

<br>(b) Pass `amount: NaN`.<br>

<br>(c) Call `fulfillPO('PO-1', -50000)` on a `100000` PO. | (a) Sorts `.500Z` (+1000) *before* `Z` (-1000), reporting `peak_operating_funding = 0` instead of `1000`!<br>

<br>(b) Returns `ZERO_OPERATING_OUTLAY`.<br>

<br>(c) Increases `total_committed_capital` to `150000`. | (a) Sorts by parsed epoch ms, reporting `peak_operating_funding = 1000`.<br>

<br>(b) Throws `E-ERR-024`.<br>

<br>(c) Throws `E-ERR-035` on non-positive `delivery_amount` or terminal PO. |
| **ADV-FIN-03** | `cashFlowEngine.ts` (XIRR / Polynomial NPV Roots) | Evaluate non-conventional cash flows `[-100, 300, -200]` ($\sum C_t = 0$, roots at $r = 0\%$ and $r = 100\%$) and all-negative `[-100, -50]`. | Function does not exist (`NOT IMPLEMENTED`). | Returns `MULTIPLE_ROOTS_DETECTED` for `[-100, 300, -200]` and `INVALID_CASH_FLOWS` for `[-100, -50]` per Charter §2.2 (`DEC-012`, `DEC-014`). |
| **ADV-PERSIST-01** | `durableRecoveryJournal.ts` (WAL Fault Injection) | Write valid entry 1 (`\n`), an extra blank line (`\n`), valid entry 2 (`\n`), and a torn tail `{"entry_id":"rec:ent:3"`. Reopen with `TRUNCATE_TORN_TAIL`. | `validBytesLength` skips the blank line's byte, so `ftruncateSync` slices off the trailing `\n` of entry 2 (or slices into entry 2 if multiple blank lines exist). | Preserves entries 1 and 2 intact with trailing `\n` and unbroken hash chain. |
| **ADV-PERSIST-02** | `durableRecoveryJournal.ts` (`CrashRecoveryEngine.recoverDurable`) | (a) WAL has Fill 1 (`BUY 100`, no `PORTFOLIO_APPLIED` marker) followed by Fill 2 (`SELL 100`, with `PORTFOLIO_APPLIED` marker); checkpoint is empty.<br>

<br>(b) Pass a journal where constructor normalization failed (`isPoisoned === true`) into `recoverDurable`. | (a) Boundary 3 loop processes Fill 2 (`SELL 100`) *before* Fill 1 (`BUY 100`), crashing with `E-ERR-042: INSUFFICIENT_INVENTORY`, and double-counts Boundary 3 fills.<br>

<br>(b) Mutates `portfolio` in memory before throwing `E-ERR-024: JOURNAL_POISONED`. | (a) Replays Fill 1 then Fill 2 in chronological order; `recovered_fills_count + skipped_duplicate_fills_count === 2`.<br>

<br>(b) Rejects poisoned journal before any portfolio mutation. |
| **ADV-SIM-01** | `simulationPipeline.ts` & `engine.ts` (Property & Concurrency) | Register a verified offer with `available_quantity: 100, minimum_order_quantity: 10` and send 5 market ticks (`bid_quantity: 100`) at the same millisecond timestamp (or consecutive timestamps). | Same-millisecond ticks crash with `E-ERR-039: IDEMPOTENCY_CONFLICT`; consecutive-millisecond ticks buy and sell 500 units from a 100-unit offer. | Total executed quantity across all ticks for `offer_id` never exceeds `offer.available_quantity` (`100`); same-millisecond ticks have distinct `intent_id`s. |
| **ADV-SEC-01** | `localWebSocketTransport.ts` & `feedHandler.ts` (Abuse / DoS) | Send tick 1 (`sequence: "1"`) followed by tick 2 (`sequence: "1000000000"`) or `sequence: "not-a-number"` or `bid_quantity: -50`. | `sequence: "1000000000"` triggers `REPLAY_REQUEST` loop of $10^9$ iterations freezing Node.js; `"not-a-number"` throws unhandled `SyntaxError` in `BigInt()`; `-50` is accepted. | Rejects replay ranges exceeding `maxReplayBufferSize`, returns `INVALID_FORMAT` on non-canonical sequences, and rejects non-positive quantities. |

### Output 6 — Prioritized Remediation Plan

| Priority | Item & Affected Findings | Dependencies | Scope & Concrete Action | Acceptance Criteria | Governance / ADR / Owner Auth Required |
| --- | --- | --- | --- | --- | --- |
| **P0** | **P0-1: Gateway Receipt & Attester Authority Cryptographic Fix** (`ARGON-CRYPTO-001`, `ARGON-CRYPTO-002`, `ARGON-SPEC-001`) | Owner approval of Spec Erratum v1.14 | Update `claims.ts`, `gate.ts`, `atomicPromotion.ts`, and Spec §3.2–§3.3 so gateway receipts bind full `ClaimSigningPayload` SHA-256 (`claim_signing_payload_sha256`), verify `operator_id`/`operator_role`, and `validateAttesterAuthority` rejects `compromised: true` and missing `revoked_at_utc` fail-closed. | `ADV-CRYPTO-01` and `ADV-CRYPTO-02` pass; end-to-end gateway promotion and post-lock revalidation tests pass. | **Requires Owner Authorization & Gate M1 Spec Erratum v1.14** |
| **P0** | **P0-2: FX Oracle Registry Authentication & Decimal Scale Validation** (`ARGON-FIN-001`, `ARGON-SPEC-001`) | Owner approval of Spec Erratum v1.14 | Update `src/canonical/currency.ts` (`validateFXReceiptAtPointOfUse` & `convertMoneySubunitsExact`) and Spec §2.1 to verify `oracle_public_key_hex` against registered `CRYPTOGRAPHIC_ORACLE` principals and enforce exact `rateScale` decimal parsing. | `ADV-FIN-01` passes; unregistered/revoked/compromised oracle keys and malformed/under-scaled rates throw `E-ERR-008` / `E-ERR-024`. | **Requires Owner Authorization & Gate M1 Spec Erratum v1.14** |
| **P0** | **P0-3: Wire 18-Tuple Allowlist into Promotion Gate & Dual-Ledger Reverse Guard** (`ARGON-EVID-001`, `ARGON-PERSIST-002`) | P0-1 | Call `validateEvidenceAllowlistEligibility` in `gate.ts` and `atomicPromotion.ts`; add 4D fields to `ResolvedEvidenceEnvelope`; implement `enforceSimulationLedgerWrite` (`E-ERR-025`) and 300s ticket check in `actualsGuard.ts`. | `PROMO-ALLOW-REJECT-011`, `CLAIM-EVID-MISMATCH-008`, and all 6 `SUITE-06` tests (`ACTUALS-GUARD-001`..`TEST-CONCURRENCY-NONCE-01`) pass. | **Requires Owner Authorization** (conforms to existing frozen spec) |
| **P0** | **P0-4: Disable Unreviewed Auto-Commit Daemon & Remove `GIT_PAT_SECRET` Env Injection** (`ARGON-SEC-001`, `ARGON-GOV-004`) | None | Remove `env["GIT_PAT_SECRET"] = token` from `scripts/sync_repos.py`; restrict `GIT_ASKPASS` to remote push/fetch; remove automatic `git add -A` daemon commits; align `.gitignore` and `FORBIDDEN_FILES` across both repos. | Zero secrets in subprocess `env` or `argv`; `Eulerpool.txt` and `Alpaca_Key.txt` blocked in both repos. | **Requires Owner Authorization** |
| **P1** | **P1-1: Financial Engine Subunit Refactor, Two-Tier Clearing, PO Lifecycle & XIRR Solver** (`ARGON-FIN-002`) | P0-2, Owner decision on transient recovery | Refactor `src/financial/cashFlowEngine.ts` to integer subunits/`CanonicalMoney`, fix timestamp sorting to parsed epoch ms, implement Two-Tier Clearing (`B_clearing` vs `B_bank`), fix `CommittedCapitalManager` (`amendPO`, positive amounts, terminal `FULFILLED`), and implement Charter §2.2 XIRR solver. | `ADV-FIN-02`, `ADV-FIN-03`, `FIN-GROSS-CLEARING-TIER-037`, `FIN-ROPF-PEAK-007`, `FIN-CONV-HPR-008`, and `FIN-PO-NETTING-003` pass. | **Requires Owner Decision** on transient zero-crossing recovery semantics |
| **P1** | **P1-2: File-Backed WAL Byte Accounting, Pre-Truncation Integrity & Single-Pass `recoverDurable**` (`ARGON-PERSIST-001`) | None | Fix `FileBackedDurableRecoveryJournal` byte offset tracking, verify prefix hash chain before `ftruncateSync`, check `getIsPoisoned()` before mutating `portfolio` in `recoverDurable`, and unify Boundary 1–3 into one chronological loop. | `ADV-PERSIST-01` and `ADV-PERSIST-02` pass; `recovered + reconciled + skipped === unique_fills`. | **Requires Owner Authorization** |
| **P1** | **P1-3: Simulation Pipeline Offer Depletion, Intent ID Disambiguation & Complete State Digest** (`ARGON-SIM-001`) | None | Track remaining offer quantity in `SimulationPipeline`, include event/sequence counter in `intent_id`, compute/verify JCS SHA-256 on all intents, use `divideHalfEven` for WACB, validate checkpoints on restore, include full journals/orders in `computeStateDigest()`, and add `scripts/**/*` to `tsconfig.json`. | `ADV-SIM-01` passes; `tsc --noEmit` passes with `scripts/**/*` included. | **Requires Owner Authorization** |
| **P1** | **P1-4: Governance Ledger, Conformance Report Reconciliation & Missing 73 Spec Tests** (`ARGON-GOV-001..003`, `ARGON-TEST-001`) | P0-1..P1-3 | Record `GATE_AUTHORIZATION_LEDGER.md`, reconcile `POC-001-M3-CONF-001` and `README.md`, remove duplicate spec files in `Market-HFT-OS/AG/`, and implement the 73 missing §8.1–§8.2 test cases. | All 111 Gate M1 tests + Gate M2/M3 suites pass; zero stale counts in `README.md` or `ADRs`. | **Requires Owner Authorization & Gate Sign-Off Ledger** |
| **P2** | **P2-1: WebSocket & Feed Handler DoS Hardening & Offer Stream Hash Chaining** (`ARGON-SEC-002`, `ARGON-PERSIST-002`) | P1-2 | Cap `pendingGapBuffer` and `REPLAY_REQUEST` range (`toSeq - fromSeq <= maxReplayBufferSize`); validate feed sequences and quantities; add `previous_event_hash` chaining to `offer_stream_events`; reconcile PostgreSQL DDL with Spec §4.1. | `ADV-SEC-01`, `STREAM-GEN-001`, and `STREAM-ERR-002` pass against production classes. | **Requires Owner Decision** on canonical PostgreSQL DDL |
| **P3** | **P3-1: Read-Only Operator Diagnostic CLI/HTML Report Wireframe** (`ARGON-UX-001`) | P1-1..P1-4 | Design a zero-dependency read-only diagnostic status exporter showing Mode/Kill-Switch state, Paper vs. Actuals ledger ratio, 4D evidence badges, and `DATA REQUIRED` flags. | Operator diagnostic view passes accessibility and epistemic-separation checklist. | **Requires New ADR & Explicit Owner Scope Approval** |

### Output 7 — Two Antigravity Review Notes

Both self-contained review notes have been generated and opened in Canvas:

1. **`ARGON_REVIEW_NOTE_MARKET_HFT_OS.md`**: Contains the exact `Market-HFT-OS` baseline (`a1bd3599e21dfb79e45df3e6c189d18c781fc5cb`), file/line-referenced findings (`ARGON-CRYPTO-001` through `ARGON-TEST-001`), required engineering corrections, acceptance criteria, prohibited actions, and unresolved owner decisions.
2. **`ARGON_REVIEW_NOTE_ADRS.md`**: Contains the exact `ADRs` baseline (`c52f66854b695320a0f5ffb0144c29bf72c91e38`), specification and governance findings (`ARGON-SPEC-001`, `ARGON-GOV-001` through `ARGON-GOV-004`), required specification errata (`v1.14`) and report reconciliations, acceptance criteria, prohibited actions, and unresolved owner decisions.

### Final Decision & Next Steps

**Overall Disposition:**
`BLOCKED — MATERIAL SAFETY/CORRECTNESS DEFECTS`
*(Note: Concurrent governance and specification conflicts `ARGON-SPEC-001` and `ARGON-GOV-001..003` are also active blockers and must be resolved alongside the code defects.)*

* **What the Human Owner Should Do Next**:
1. Review and decide on the four open governance/specification questions in `ARGON_REVIEW_NOTE_MARKET_HFT_OS.md` §6 and `ARGON_REVIEW_NOTE_ADRS.md` §6: (a) authorizing **Gate M1 Specification Erratum v1.14** to fix the three embedded specification defects (§2.1 FX oracle registry check, §3.2 `validateAttesterAuthority` compromise/revocation check, and §3.3 `claim_signing_payload_sha256` full-payload binding), (b) choosing the post-outlay recovery rule for subsequent operating deficits, (c) choosing the canonical PostgreSQL DDL (`postgresAdapter.ts` vs Spec §4.1), and (d) restricting `scripts/sync_repos.py` to manual/reviewed operation.
2. Authorize Antigravity to execute the **P0** and **P1** remediation items in a dedicated branch before any Gate M3 sign-off.


* **What Antigravity May Safely Investigate Now (Read-Only)**:
* Reproduce the 5 standalone counterexamples (`ARGON-FIN-001`, `ARGON-CRYPTO-001`, `ARGON-CRYPTO-002`, `ARGON-FIN-002`, `ARGON-PERSIST-001`) in a read-only test harness.
* Draft the proposed text for **Gate M1 Specification Erratum v1.14** and `GATE_AUTHORIZATION_LEDGER.md` for Owner review without overwriting the frozen specification commit.


* **What Remains Prohibited Until Explicitly Authorized by the Owner**:
* Do not mark Gate M3 as closed or advance to Gate M4 / live execution.
* Do not run `scripts/sync_repos.py --daemon` or auto-commit/push unreviewed working-tree changes to `main`.
* Do not modify or import `_salvage/AIStudio/` or `_salvage/external/`, connect to any external exchange, or alter the frozen Gate M1 specification without a versioned Owner-approved erratum.