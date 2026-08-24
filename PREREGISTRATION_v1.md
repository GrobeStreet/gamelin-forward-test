# GAMELIN Forward-Test — Pre-Registration v1

**STATUS: DRAFT — NOT REGISTERED — RACE 001 LOCKED**

**Registered:** pending Canon v1.0 freeze

**Model version at kickoff:** pending

**methodology_hash:** pending

**Author:** Robert "Bobby" Morong — GAMELIN

This document is the honesty contract for the first public forward test. It must be completed and publicly committed **before** Race 001 is logged. Any material change after registration creates a new dated version; records generated under a prior version remain graded under that prior version.

## 1. What is being tested

Whether GAMELIN's frozen, gated selections, generated before post under a fixed decision rule, add information beyond the pari-mutuel market and produce economically meaningful results under real settlement.

This is a **forward test**, not a backtest. Historical results motivate the design but do not count toward this record.

## 2. Scope

Working scope carried forward from the existing preregistration design:

- Bet type: **WIN only** for the primary record.
- Market: U.S. pari-mutuel thoroughbred win pools.
- Initial circuit: **Del Mar Thoroughbred Club**, unless P0 source/data review requires an amendment before registration.
- Headline stake: **1.00 unit flat per qualifying BET**.
- No exotics in this ledger.
- No variable discretionary staking in the headline record.

## 3. Decision rule

**PENDING CANONICALIZATION.**

The historical preregistration proposed a deterministic BET gate requiring all of:

1. qualifying conviction tier;
2. model-vs-market edge at or above a fixed threshold;
3. non-negative expected value at decision odds.

P0 must verify that this gate is exactly compatible with the production v7.0 Conviction engine and freeze the final thresholds before registration.

Until then, **no race may be counted.**

Canonical policy direction:

- GAMELIN may always produce a projected winner/ranking.
- A wager is recommended only when the registered gate passes.
- If the gate fails, the decision is **PASS** and is retained in the record.

## 4. Valid-race definition

Final eligibility criteria will be frozen before registration. At minimum, an eligible race must have:

- correct circuit/race identity;
- at least five active runners unless Canon explicitly defines otherwise;
- complete required pre-race model inputs under the registered data mode;
- a market snapshot with an auditable observation timestamp;
- a GAMELIN decision timestamp strictly before official post/off time under the registered logging convention.

Any excluded or missed race must be recorded with a reason rather than silently removed.

## 5. Logging protocol

1. **Pre-race record committed before post.**
2. Every record carries `model_version` and `methodology_hash`.
3. The pre-race block is immutable after commitment.
4. Official settlement is appended afterward in a separate settlement record.
5. Missing cards/races are logged as gaps with reasons.
6. BET and PASS decisions are both retained.

## 6. Settlement

- Settle WIN bets from official final pari-mutuel win payoffs.
- Takeout is therefore embedded in the observed payoff.
- Scratched selections are void and marked as such.
- Cancelled/non-run races are void and marked.
- Dead heats follow official settlement.

## 7. Metrics

The primary evidence suite will include:

- probability calibration / reliability;
- Brier score and Brier skill versus the de-vigged market at the registered decision timestamp;
- a market-relative probability comparison / Model-Beat-Market measure;
- flat-stake net ROI with bootstrap confidence interval;
- maximum drawdown;
- longest losing streak;
- BET rate and PASS rate;
- data-freshness / timestamp integrity reporting.

Baselines must be declared before Race 001 and may include market probability at the same timestamp and blind-favorite behavior.

## 8. Pre-declared segments

The earlier design proposed only the following pre-registered cuts:

- conviction tier;
- odds bands;
- field-size bands;
- surface.

P0 will verify/freeze the exact bins before registration. Any later slice is exploratory and must be labeled as such.

## 9. Versioning

Every prediction carries a model version and methodology hash. If the model, thresholds, required inputs, race eligibility, settlement rule, or primary metrics change, a new preregistration version is required. Prior records are never regraded under the new method.

## 10. Evaluation point

The existing design sets the first formal public readout at the later of:

- **200 qualifying BETs**, or
- **60 calendar days**.

Interim statistics may be displayed but must be labeled insufficient for the registered ROI conclusion.

## 11. Falsification

A failed result is publishable evidence.

If the registered test fails to show improvement over the declared market baseline and/or the ROI confidence interval does not support a positive-return claim, GAMELIN will not relabel or remove the result. The result belongs in the permanent record and, where appropriate, the `nulls/` directory.

## 12. Registration gate

This file becomes active only when all of the following are complete:

- [ ] `CANONICAL_MODEL.md` frozen
- [ ] final decision thresholds frozen
- [ ] exact input/data mode frozen
- [ ] corpus/claim reconciliation complete
- [ ] methodology artifact generated
- [ ] SHA-256 methodology hash inserted here
- [ ] registration date/time inserted here
- [ ] baseline definitions frozen
- [ ] ledger schema committed
- [ ] settlement schema committed

**Until every box is complete: Race 001 is forbidden.**
