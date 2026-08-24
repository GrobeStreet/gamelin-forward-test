# GAMELIN Model Lineage

Status: **P0 canonicalization record — Canon v1.0 model selected**

This document preserves the known model generations that appeared in GAMELIN research/specification artifacts. Its purpose is to prevent silent model drift and make the canonical choice explainable.

## Generation A — early fitted three-factor specification

Documented form:

```text
score = 2.20 * market_percentile
      + 0.36 * class_percentile
      + 0.45 * recent_speed_percentile
      - 3.75
```

Inputs:
- normalized market probability / within-race market percentile
- Equibase class rating / within-race class percentile
- recent speed, generally average of prior three Speed Figures / within-race percentile

Associated product framing:
- projected winner from the highest score
- explicit race-type confidence gate
- PASS in weaker race classes/conditions

Disposition: **historical / superseded for Race 001.**

Reason: this was a real fitted stage of the project, but later final-engine work explicitly superseded it with the optimized Conviction-era model now matched in production.

## Generation B — intermediate three-factor fitted specification

Documented form:

```text
score = 1.738 * market_pct
      + 0.387 * class_pct
      + 0.585 * speed_pct
      - 3.732
```

Associated handoff notes describe this as walk-forward validated on 6,467 U.S. races with a 1,730-race holdout.

Disposition: **historical / superseded for Race 001.**

Reason: this coefficient set appears in an intermediate handoff and is not the formula used by the final June 2 Conviction sync or current production v7.0 implementation.

## Generation C — final Conviction engine / Canon v1.0

The final June 2 engine sync explicitly identifies a **Canon Engine** and says it supersedes the earlier v6 agreement-only framing. Current production identifies itself as:

```text
GAMELIN Evidence Engine · v7.0 Conviction Index
```

The production source and final engine sync match on the winner model:

```text
logit = 1.838 * market_pct
      + 0.582 * class_pct
      + 0.065 * speed_pct
      + 0.318 * (agreement / 3)
      + 0.409 * premium
      - 0.062 * midpurse
      + 0.018 * turf
      - 3.454

win_prob = softmax(logit across the active field)
```

Conviction Index:

```text
CONVICTION = (mean(z_market,z_class,z_speed)
              + min(z_market,z_class,z_speed))
             * (1 + 0.5 * agreement)
```

Production absolute Conviction bands:

```text
raw >= 3.25                         -> ELITE, multiplier 1.0
raw >= 2.20                         -> STRONG, multiplier 0.8
raw >= 1.10                         -> BETTABLE, multiplier 0.5
agreement >= 2 and raw >= 0.25      -> 2/3 SIGNAL, multiplier 0.5
otherwise                           -> LOW, multiplier 0
```

Production also excludes runners below 5% de-vigged market probability from the primary Conviction win-bet candidate set.

Disposition: **SELECTED AND FROZEN AS `GAMELIN-CANON-v1.0` MODEL COMPONENT.**

The complete frozen analytical specification is in `CANONICAL_MODEL.md`.

## P0 finding: the production `ev` name is semantically wrong

Current production assigns:

```text
ev = model_prob - market_prob
```

That is a **probability edge**, not monetary expected value. Canon therefore renames it:

```text
edge_pp = model_prob - market_prob
```

True decision-price EV is separately defined as:

```text
ev_decision = model_prob * decimal_odds - 1
```

This is a terminology/correctness reconciliation, not a newly fitted model change. The registered forward-test gate must use the correct quantity names and cannot call probability edge monetary EV.

## Decision-policy drift resolved

Two incompatible product rules appeared historically:

1. **PASS doctrine:** always provide a race read / likely winner, but do not recommend money when the evidence/price gate fails.
2. **Always-bet doctrine:** always name a winner and always recommend at least one wager even when no positive-value opportunity exists.

For the registered evidence record, P0 resolves this in favor of:

> **Always preserve the race read. Never force a primary wager.**

The always-bet specification is historical and superseded for the public forward test.

## Remaining registration work

The model itself is now selected. Race 001 remains locked because the following still must be frozen:

- exact forward-test input/data source;
- exact decision-time/freshness protocol;
- final primary BET/PASS price gate using true `ev_decision`;
- canonical corpus/claim wording;
- final methodology artifact + SHA-256;
- completed registered preregistration.
