# GAMELIN Forward Test

> **P0: GAMELIN Canonicalization + Forward-Test Launch**

This public repository is the append-only evidence home for GAMELIN's canonical forward test.

GAMELIN is being evaluated as a market-aware horse-racing decision engine. The purpose of this repository is not to publish cherry-picked winning tickets. It is to preserve the full pre-race record — including BET, PASS, null, losing, void, and excluded outcomes — under fixed, versioned rules that were committed before the results were known.

## P0 gate

**Race 001 may not be logged until all four gates are complete:**

1. Canonical model/specification reconciled and frozen.
2. Canonical methodology hash generated.
3. Forward-test pre-registration completed with the frozen version/hash and committed publicly.
4. Ledger schema and append-only settlement procedure established in this repository.

Until those conditions are met, this repository is in **CANONICALIZATION** state, not active forward-test state.

## Repository contract

- No post-result edits to a pre-race prediction block.
- Every eligible race under the registered scope is logged or explicitly recorded as a gap/exclusion.
- PASS decisions remain part of the record.
- Settlements are appended after official results; they do not overwrite the original prediction.
- Model/rule changes create a new dated/versioned methodology. Prior records remain graded under the methodology that generated them.
- Losing and null results are preserved.
- Performance is compared with the market and declared baselines, not just raw winner percentage.

## Planned structure

- `CANONICAL_MODEL.md` — frozen GAMELIN specification once reconciliation is complete.
- `MODEL_LINEAGE.md` — documented history of prior model generations and why Canon differs.
- `DATA_PROVENANCE.md` — dataset/source accounting and limitations.
- `CLAIMS_REGISTER.md` — approved, qualified, deprecated, and forbidden public claims.
- `PREREGISTRATION_v1.md` — public forward-test honesty contract.
- `methodology/` — canonical hash and version artifacts.
- `ledger/` — pre-race append-only records.
- `settlements/` — official post-race grading records.
- `reports/` — scheduled readouts and calibration reports.
- `nulls/` — failed hypotheses and falsified forward-test results.

## Current state

**CANONICALIZATION — Race 001 locked.**

The current production candidate is GAMELIN Evidence Engine v7.0 / Conviction Index, but it is not declared canonical until its formulas, decision rules, claims, evidence counts, and provenance are reconciled against the underlying research and historical specifications.
