# GAMELIN Forward-Test — Pre-Registration v1

**STATUS: DRAFT — NOT REGISTERED — RACE 001 LOCKED**

**Registered:** pending final input-rights/capture freeze

**Model version at kickoff:** `GAMELIN-CANON-v1.0`

**methodology_hash:** pending

**Author:** Robert "Bobby" Morong — GAMELIN

This document is the honesty contract for the first public forward test. It must be completed and publicly committed **before** Race 001 is logged. Any material change after registration creates a new dated version; records generated under a prior version remain graded under that prior version.

## 1. What is being tested

Whether `GAMELIN-CANON-v1.0` gated WIN selections, generated before post under a fixed rule, add information beyond the U.S. pari-mutuel market and produce positive flat-stake results after real tote settlement.

This is a **forward test**, not a backtest. Historical results motivate the frozen model and thresholds but do not count toward this record.

The test intentionally separates three questions:

1. Are Canon probabilities calibrated?
2. Do Canon probabilities add information beyond the market?
3. Do the fixed BET decisions return positive flat-stake ROI at official settlement?

## 2. Scope

- Bet type: **WIN only** for the primary record.
- Market: **U.S. pari-mutuel thoroughbred win pools**.
- Initial circuit: **Del Mar Thoroughbred Club**.
- Headline stake: **1.00 unit flat per qualifying BET**.
- PASS stake: `0.00` units.
- At most **one primary BET per race**.
- No exotics in this ledger.
- No variable discretionary staking in the headline record.

## 3. Canon model

The frozen analytical model is defined in `CANONICAL_MODEL.md`.

Key distinction:

```text
projected_winner     = runner with highest model_prob
conviction_candidate = highest conviction_raw among eligible candidates
```

They may be different horses.

The public ledger records both the race ranking and the action decision.

## 4. Probability and price quantities

For each active runner with observed decimal odds:

```text
raw_implied_prob_i = 1 / decimal_odds_i
market_prob_i      = raw_implied_prob_i / sum_j(raw_implied_prob_j)
edge_pp_i          = model_prob_i - market_prob_i
ev_decision_i      = model_prob_i * decimal_odds_i - 1
```

`edge_pp` is a probability edge. `ev_decision` is expected profit per 1 unit at the observed decision price.

The production consumer variable historically named `ev` but equal to `model_prob - market_prob` is **not** treated as monetary EV in this registered test.

## 5. Primary BET/PASS gate — frozen

The primary candidate pool contains active full-model runners satisfying:

```text
market_prob >= 0.05
```

Choose the runner with the highest `conviction_raw` from that pool.

That runner is a **BET** if and only if all of the following hold:

1. **Full Canon input mode is valid** for the race under §6.
2. The runner is `high_conviction = true` under the absolute Canon bands:
   - `conviction_raw >= 3.25`, or
   - `conviction_raw >= 2.20`, or
   - `conviction_raw >= 1.10`, or
   - `agreement >= 2 AND conviction_raw >= 0.25`.
3. `edge_pp >= +0.02`.
4. `ev_decision >= 0` at the registered decision odds.

Otherwise the race's primary action is **PASS**.

No human discretion may upgrade a PASS to BET.

A race can still have a projected winner and full ranking when the primary action is PASS.

### Why the 2-point edge floor remains

The earlier preregistration design declared a `+0.02` model-vs-market probability floor before any live result was seen. Canon retains that pre-existing threshold rather than optimizing it after forward outcomes.

### Why true EV is also required

Positive de-vigged probability edge does not by itself prove that the displayed price clears pari-mutuel takeout/overround. The separate `ev_decision >= 0` test prevents the ledger from calling a horse a value WIN bet when the observed price is still economically negative under the model.

## 6. Valid-race definition — model requirements frozen, source rights pending

A race is model-eligible only if all of the following are true at the registered decision timestamp:

- Del Mar U.S. thoroughbred win-pool race;
- at least **5 active runners**;
- race identity and official scheduled post are resolved;
- scratches known at the decision snapshot are applied;
- observed odds are available for **every active runner**;
- ClassRating is available for **every active runner** from the registered rights-cleared source;
- last-three-prior SpeedFigure average is available for **every active runner** under the registered rights-cleared source/parser;
- no forbidden/post-race field is used;
- the probability field normalizes successfully;
- the pre-race record is committed strictly before official off/post under the final timing convention.

A race failing the full-model requirements is **EXCLUDED**, not silently dropped. The exclusion and reason are logged.

Production market-only or partial-PP fallbacks do not qualify for the headline Canon v1.0 forward ledger.

The source/timing boundary is documented in `DATA_INPUT_PROTOCOL.md`. Current ClassRating/SpeedFigure rights and complete coverage remain a registration blocker.

## 7. Decision timestamp and odds source

The intended official Del Mar market source is:

`https://www.dmtc.com/handicapping/odds`

The target decision state is:

> **the first complete official Del Mar odds snapshot observed while the source displays `5 MTP`.**

The official changes source is:

`https://www.dmtc.com/racing/changes`

The no-discretion principle is frozen: once the first valid 5-MTP snapshot is observed, a later price may not replace it because it is more favorable.

**Still pending before registration:** the reproducible capture implementation, access-term verification, raw/hash audit artifact behavior, and the exact rule if the implementation fails to obtain a complete 5-MTP snapshot. The current direction is EXCLUDE rather than substitute a discretionary later price.

Until those mechanics are tested and frozen, **Race 001 is forbidden.**

## 8. Logging protocol

1. **Pre-race record committed before post/off.**
2. Every record carries `model_version` and `methodology_hash`.
3. The pre-race block is immutable after commitment.
4. Official settlement is appended afterward in a separate settlement record.
5. Missing cards/races are logged as gaps or exclusions with reasons.
6. BET, PASS, and EXCLUDED states are all retained.
7. The projected winner/ranking is retained even when the action is PASS.
8. No result is deleted because it is unfavorable.

The public schema is frozen at `ledger/schema-v1.json`.

## 9. Settlement

- Settle qualifying WIN BETs from the **official final pari-mutuel win payoff**.
- Takeout is therefore embedded in the observed payoff.
- Scratched selections are void and marked as such.
- Cancelled/non-run races are void and marked.
- Dead heats follow official settlement.
- A decision-price EV estimate is never substituted for actual settled P&L.

The public schema is frozen at `settlements/schema-v1.json`.

## 10. Primary metrics

Report from the start:

- probability calibration / reliability;
- Brier score;
- Brier skill versus the de-vigged market baseline at the registered decision timestamp;
- log loss vs. the same market baseline;
- Model-Beat-Market (`model_prob - final_market_prob`) summary where final-market probability can be reconstructed consistently;
- BET count, PASS count, EXCLUDED count, and coverage rate.

Report with appropriate sample-size caveat:

- flat-stake net ROI;
- bootstrap 95% CI on per-bet P&L using 10,000 resamples;
- maximum drawdown;
- longest losing streak.

## 11. Baselines — frozen

The registered comparison set is:

1. **De-vigged market probability** from the same registered decision snapshot.
2. **Blind market favorite** at the same decision snapshot for winner/hit-rate and settlement comparisons where applicable.
3. **0% net ROI** as the economic breakeven line after real tote settlement.

No new baseline may replace a losing registered baseline after results are known.

## 12. Pre-declared segments — frozen

Registered descriptive cuts are limited to:

### Conviction band
- ELITE
- STRONG
- BETTABLE
- 2/3 SIGNAL

### Decision odds
- `<= 2/1`
- `> 2/1 to 5/1`
- `> 5/1 to 10/1`
- `> 10/1`

### Field size
- `5–7`
- `8–10`
- `11+`

### Surface
- dirt
- turf

Any other slice is exploratory and must be labeled **EXPLORATORY / NOT PRE-REGISTERED**.

## 13. Model versioning

Every prediction carries `model_version` and `methodology_hash`.

Any post-registration change to:

- model formula or features;
- Conviction formula/bands;
- 5% candidate floor;
- +2pp edge floor;
- true-EV threshold;
- candidate-selection rule;
- required input mode/source;
- decision-time/freshness rule;
- race eligibility;
- settlement;
- primary metrics or registered segments;

requires a new preregistration version.

Prior records are never regraded under the new method.

## 14. Evaluation point

The first formal public readout occurs at the later of:

- **200 settled qualifying BETs**, or
- **60 calendar days after Race 001**.

Interim statistics may be displayed but must be labeled insufficient for the registered ROI conclusion.

Calibration and process-integrity metrics may be reported from the start.

## 15. Falsification

A failed result is publishable evidence.

At the first formal readout:

- if Brier skill vs. the registered market baseline is `<= 0`, Canon v1.0 has not demonstrated probability improvement over the market on this test;
- if the ROI bootstrap 95% CI includes or lies below `0`, positive ROI is not demonstrated at the registered threshold.

These findings must be published as observed. They may motivate a future v2 but may not be erased or retroactively re-gated.

## 16. Registration gate

- [x] `CANONICAL_MODEL.md` model component frozen
- [x] Canon decision candidate and conviction thresholds frozen
- [x] probability-edge vs. true-EV semantics reconciled
- [x] full-model feature requirements frozen
- [x] corpus/claim reconciliation completed for public headline wording
- [x] baseline definitions frozen
- [x] registered segment bins frozen
- [x] intended official Del Mar decision-odds source selected
- [x] target decision state fixed at first complete `5 MTP` snapshot
- [x] ledger file schema finalized against this preregistration
- [x] settlement schema finalized against this preregistration
- [ ] rights-cleared complete ClassRating/SpeedFigure source frozen
- [ ] exact missing-history behavior reproduced/frozen
- [ ] 5-MTP capture mechanism tested, non-discretionary, and access-term compliant
- [ ] odds-source failure/exclusion timing rule finalized in implementation
- [ ] methodology artifact generated
- [ ] SHA-256 methodology hash inserted here
- [ ] registration date/time inserted here
- [ ] final preregistration committed before Race 001

**Until every box is complete: Race 001 is forbidden.**
