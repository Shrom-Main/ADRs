# ADR-0003: File-Backed WAL Durability, Torn-Tail Recovery Policy, and Crash Recovery Contract

* **Status:** Accepted
* **Date:** 2026-10-14
* **Deciders:** Project Owner, System Architect, Persistence & Recovery Lead
* **Technical Domain:** Persistence Engine, Write-Ahead Log (WAL), Crash Recovery, Durability Guarantees

---

## Context and Problem Statement

Gate M1 specified in-memory journal records for recovery testing. To achieve physical durability under Gate M3, the operating system requires an on-disk Write-Ahead Log (WAL) capable of surviving sudden process termination (crash exit, SIGKILL, power interruption) without loss of committed events or state corruption.

Key technical requirements identified during Gate M3 development and subsequent audits (`ARGON-REV-POC001-20261014`):
1. **Append-Only File-Backed Journal:** Mutations (orders, fills, checkpoints) must be flushed and fsynced to disk prior to notifying callers.
2. **Torn-Tail Handling:** Sudden process termination during a write can leave an un-flushed partial JSON record at the physical end of the file.
3. **Delimiter Accounting & Normalization:** Valid JSON records written without a trailing newline or written with CRLF (`\r\n`) delimiters must have exact physical byte accounting to prevent corrupted concatenations upon subsequent append operations.
4. **Poisoning on Sync Failure:** If an `fsyncSync` or write fails, the in-memory journal must enter a fail-closed poisoned state, preventing further corrupt mutations.
5. **Separate-Process Recovery Parity:** Restarted processes must recover full portfolio state, fills, and canonical hash digests identical to an uninterrupted benchmark.

## Decision Drivers

1. Absolute deterministic recovery from cold storage without data corruption.
2. Safe recovery from uncompleted tail writes without sacrificing fail-closed interior corruption detection.
3. Cross-platform delimiter robustness (Linux LF `\n` vs. Windows CRLF `\r\n`).
4. Fail-closed defense against partial disk flushes.

## Considered Options

* **Option 1 (Strict Fail-Closed on Any Incomplete Byte):** Reject the entire log and refuse to start if any trailing partial line or missing newline is detected.
  - *Deficiency:* Process termination mid-buffer results in permanent unrecoverable state, requiring manual operator surgery even for uncommitted transient tails.
* **Option 2 (Unchecked Append Mode):** Open files in `a` mode without inspecting existing boundaries.
  - *Deficiency:* Concatenates subsequent JSON records directly onto unterminated trailing records, permanently corrupting the log.
* **Option 3 (Torn-Tail Truncation with Boundary Normalization):**
  - Parse existing valid records.
  - If a valid terminal record lacks a terminating newline, normalize it by writing `\n` and calling `fsyncSync`.
  - If the tail is malformed (partial JSON), truncate to the last known valid boundary when `tornTailPolicy: 'TRUNCATE_TORN_TAIL'` is set.
  - If interior corruption exists, fail closed immediately (`E-ERR-046`).
  - Accurately calculate delimiter byte length (`\n` = 1 byte, `\r\n` = 2 bytes).

## Decision Outcome

Chosen option: **Option 3**. We adopt `FileBackedDurableRecoveryJournal` with `TRUNCATE_TORN_TAIL` policy, explicit delimiter normalization, and live-state poisoning.

### Physical WAL Contract Specifications

1. **Delimiter Handling:**
   - Lines are parsed and sanitized by stripping trailing carriage returns (`\r`).
   - Delimiter byte lengths are explicitly charged (`\r\n` = 2 bytes, `\n` = 1 byte).
   - Valid unterminated terminal records are normalized on disk with an explicit newline and `fsyncSync` before opening for write.
2. **Torn-Tail Truncation Policy:**
   - **`TRUNCATE_TORN_TAIL` (Default):** Invalid partial bytes occurring after the last valid record are truncated using `fs.truncateSync`. The journal continues appending from the safe boundary.
   - **`FAIL_CLOSED`:** Rejects startup if any non-whitespace unparsed bytes remain at the end of the log.
   - **Interior Corruption:** Any invalid JSON, sequence gap, or hash-chain break occurring *prior* to valid records triggers immediate fail-closed error `E-ERR-046: JOURNAL_CORRUPTED`.
3. **Poisoning on I/O Failure:**
   - If `fs.writeSync` or `fs.fsyncSync` throws an exception, the journal is marked poisoned (`isPoisoned = true`), its file descriptor is closed, and all subsequent append/query calls throw `E-ERR-047: JOURNAL_POISONED`.
4. **Crash Recovery Parity Contract:**
   - Recovery procedure:
     1. Locate latest verified checkpoint file.
     2. Verify Ed25519 checkpoint signature and unpack `PortfolioSnapshot`.
     3. Replay subsequent WAL journal entries from `checkpoint.sequence + 1`.
     4. Verify monotonic sequence progression and cryptographic hash-chain link ($H_k = \operatorname{sha256}(H_{k-1} \,\|\, JCS(E_k))$).
     5. Assert identical canonical state digest between cold-restarted process and continuous runtime.

## Traceability and Compliance

- **Implementation:**
  - `src/persistence/durableRecoveryJournal.ts` (`FileBackedDurableRecoveryJournal`)
  - `src/persistence/crashRecoveryEngine.ts` (`CrashRecoveryEngine`)
- **Regression & Conformance Tests:**
  - `tests/acceptance/suite16_crash_recovery_persistence.test.ts`:
    - `M3-WAL-VALID-UNTERMINATED-RECORD-017`
    - `M3-WAL-CRLF-DELIMITER-NORMALIZATION-018`
    - `M3-CRASH-RECOVERY-SEPARATE-PROCESS-001`
    - `M3-CRASH-RECOVERY-TORN-TAIL-TRUNCATE-002`
- **Error Codes:**
  - `E-ERR-046` (Journal corrupted / interior corruption)
  - `E-ERR-047` (Journal poisoned / I/O sync failure)
