# GAMELIN Model Lineage

Status: **P0 canonicalization working record**

This document preserves the known model generations that appeared in GAMELIN research/specification artifacts. Its purpose is to prevent silent model drift and make the final canonical choice explainable.

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

Disposition: **historical / not canonical unless reproduced and selected during P0 reconciliation.**

## Generation B — later three-factor fitted specification

Documented form:

```text
score = 1.738 * market_pct
      + 0.387 * class_pct
      + 0.585 * speed_pct
      - 3.732
```

Associated handoff notes describe this as walk-forward validated on 6,467 U.S. races with a 1,730-race holdout.

Disposition: **historical / not canonical unless reproduced and selected during P0 reconciliation.**

## Generation C — production v7.0 Conviction-era picker

The current production site identifies itself as:

```text
GAMELIN Evidence Engine · v7.0 Conviction Index
```

Current production weight family:

```text
marketPct  = 1.838
classPct   = 0.582
speedPct   = 0.065
agreement  = 0.318
premium    = 0.409
midpurse   = -0.062
```

The corresponding research handoff gives the full logistic specification as:

```text
logit = 1.838 * market_pct
      + 0.582 * class_pct
      + 0.065 * speed_pct
      + 0.318 * (agree / 3)
      + 0.409 * premium
      - 0.062 * midpurse
      + 0.018 * turf
      - 3.454

win_prob = softmax(logit across the field)
```

Conviction Index documented with this generation:

```text
CONVICTION = (mean(z_market, z_class, z_speed)
              + min(z_market, z_class, z_speed))
             * (1 + 0.5 * agree)
```

Research notes characterize conviction as the selective-betting layer rather than evidence that the raw winner picker dramatically outperforms the market.

Disposition: **current production candidate for Canon v1.0, not yet frozen.**

## Decision-policy drift that must be resolved

Two incompatible product rules appeared historically:

1. **PASS doctrine:** always provide a race read / likely winner, but do not recommend money when the gate fails.
2. **Always-bet doctrine:** always name a winner and always recommend at least one wager even when no positive-value opportunity exists.

The current production implementation already supports explicit `PASS` / `$0` outcomes while still surfacing the likely winner. P0 therefore treats the PASS doctrine as the leading candidate for Canon v1.0, subject to final reconciliation.

## P0 selection rule

Canon v1.0 will not be chosen because it is newest or because it produces the most attractive historical result. It will be chosen only after:

- the production implementation is matched exactly to a written specification;
- the source research supporting each term is identified;
- leakage safety is confirmed;
- decision-gate semantics are fixed;
- historical claims tied to superseded formulas are separated from Canon claims;
- one immutable methodology representation is generated and hashed.

Until that happens, **Race 001 remains locked.**
