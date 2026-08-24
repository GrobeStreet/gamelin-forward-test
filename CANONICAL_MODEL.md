# GAMELIN Canonical Model v1.0

**Status: MODEL COMPONENT FROZEN — FORWARD TEST NOT YET REGISTERED**

**Canonical model:** `GAMELIN-CANON-v1.0`

**Source lineage:** production `GAMELIN Evidence Engine · v7.0 Conviction Index`, reconciled against the June 2 final-engine sync. This supersedes the earlier three-factor specifications documented in `MODEL_LINEAGE.md`.

This file freezes the analytical engine that will generate the first public forward test. It does **not** by itself unlock Race 001. The input source/timing protocol, final registered action gate, methodology artifact/hash, and completed preregistration must still be frozen and committed.

## 1. Canonical purpose

GAMELIN has two distinct outputs and they must never be conflated:

1. **Winner probability / race ranking** — which runner the model considers most likely to win.
2. **Betting conviction / action** — whether the evidence is strong enough to justify a primary WIN wager at the observed price.

A likely winner can still be a PASS.

## 2. Required full-model inputs

For each active runner at the registered decision timestamp:

- `market_prob` — de-vigged win probability derived from the observed race odds and normalized across the active field.
- `market_pct` — within-race percentile rank of `market_prob`, higher = stronger.
- `class_rating` — pre-race ClassRating / Today's Horse Class Rating.
- `class_pct` — within-race percentile rank of `class_rating`, higher = stronger.
- `recent_speed` — average of the runner's last three prior pre-race Speed Figures.
- `speed_pct` — within-race percentile rank of `recent_speed`, higher = stronger.

For the registered headline forward test, a race is not full-model eligible unless the required class and recent-speed inputs are available under the frozen input protocol. Production fallback modes may remain useful to consumers but do not receive Canon v1.0 headline BET status.

### Forbidden model inputs

The following remain forbidden as pre-race predictors because the research identified them as post-race leakage or otherwise invalid for this purpose:

- same-race official finish / winner information;
- same-race payoff/result fields;
- post-race RPR/TR fields from the identified archive representation;
- any field discovered to encode the race outcome;
- any feature created using data observed after the registered decision timestamp.

## 3. Winner-probability engine

For each runner:

```text
logit = 1.838 * market_pct
      + 0.582 * class_pct
      + 0.065 * speed_pct
      + 0.318 * (agreement / 3)
      + 0.409 * premium
      - 0.062 * midpurse
      + 0.018 * turf
      - 3.454
```

Then:

```text
model_prob_i = exp(logit_i) / sum_j(exp(logit_j))
```

The projected winner is the active runner with the highest `model_prob`.

### Agreement

`agreement` is the count in `{0,1,2,3}` of the runner being tied for the field lead on:

- market probability;
- class rating;
- recent speed.

The production implementation applies the agreement term only when both class and speed are present in the field. The registered forward test requires the full-model input mode, so the denominator is three.

### Race-regime flags

The production v7.0 implementation defines:

```text
turf     = surface identifies turf/grass
midpurse = purse >= 15,000 and purse <= 40,000
premium  = purse >= 40,000 OR race class identifies stakes/stk/handicap
```

At exactly a 40,000 purse, the production logic makes both `midpurse` and `premium` true. Canon v1.0 preserves that exact behavior rather than silently changing it during preregistration.

## 4. Conviction Index

Conviction is a separate selective-betting signal.

Compute within-field z-scores for market probability, class rating, and recent speed:

```text
z_market
z_class
z_speed
```

Then:

```text
conviction_raw = (
    mean(z_market, z_class, z_speed)
    + min(z_market, z_class, z_speed)
) * (1 + 0.5 * agreement)
```

Interpretation:

- the mean represents broad signal strength;
- the minimum is a weakest-link penalty;
- agreement amplifies unanimity.

The displayed 0–100 score used by production is:

```text
conviction_score = clamp(round(50 + 10 * conviction_raw), 0, 100)
```

The display score is presentation. `conviction_raw` and the frozen thresholds below control Canon action eligibility.

## 5. Absolute conviction bands

Production v7.0 replaced within-race relative ranking as the action trigger because relative rank can make a weak field appear artificially strong.

Canonical bands:

```text
ELITE:
  conviction_raw >= 3.25
  multiplier = 1.0

STRONG:
  conviction_raw >= 2.20
  multiplier = 0.8

BETTABLE:
  conviction_raw >= 1.10
  multiplier = 0.5

2/3 SIGNAL:
  agreement >= 2 AND conviction_raw >= 0.25
  multiplier = 0.5

LOW:
  otherwise
  multiplier = 0
```

A runner is `high_conviction = true` only in the first four bands.

## 6. Longshot boundary

Production v7.0 excludes runners with de-vigged `market_prob < 0.05` from its primary Conviction win-bet candidate set. Canon v1.0 preserves that boundary for the headline WIN action layer.

The model may still rank such a runner, but it cannot be the primary registered WIN BET candidate under v1.0.

## 7. Correct probability-edge terminology

P0 found an important semantic issue in the current consumer implementation.

Production stores:

```text
a.ev = model_prob - market_prob
```

That quantity is **not monetary expected value**. It is a probability edge.

Canon terminology is therefore:

```text
edge_pp = model_prob - market_prob
```

True decision-price expected value must be calculated separately from the actual observed decimal odds:

```text
ev_decision = model_prob * decimal_odds - 1
```

Equivalent one-unit profit form:

```text
ev_decision = model_prob * (decimal_odds - 1) - (1 - model_prob)
```

These are algebraically identical.

No Canon report may call `model_prob - market_prob` monetary EV.

## 8. Projected winner vs. registered bet candidate

These may be different horses.

- `projected_winner` = highest `model_prob`.
- `conviction_candidate` = highest `conviction_raw` among active full-model runners with `market_prob >= 0.05`.

This distinction is intentional and comes from the final Conviction-engine design: win probability names the likely winner; Conviction determines whether a runner is sufficiently strong for the primary betting decision.

## 9. Canon action doctrine

The permanent doctrine is:

> **Always preserve the race read. Never force a primary wager.**

Historical "always make a bet" specifications are superseded for the registered evidence record.

The final exact headline `BET/PASS` rule will be frozen in `PREREGISTRATION_v1.md` before registration. It must use the Canon model above and must distinguish probability edge from true price EV.

Until that gate, the decision timestamp protocol, and the data-input contract are frozen, **Race 001 remains locked**.

## 10. Historical validation attached to this generation

The June 2 final-engine sync reports the following as historical/backtest validation for the final Conviction generation:

- full validated sample: `6,559` races;
- strict date holdout: top-conviction pick `31.1%` win rate and `+5.7%` ROI versus market `-3.9%`;
- bootstrap median approximately `+6%`, with `98%` of resamples positive;
- all top-conviction picks: `30.8%` win, `+4.5%` ROI, `1.26` A/E;
- top-50% Conviction subset: `35.5%` win, `+10.6%` ROI, `1.33` A/E;
- top-25%: `39.3%` win, `+13.1%` ROI, `1.36` A/E;
- top-10%: `41.6%` win, `+13.7%` ROI, `1.36` A/E;
- agreement = 3: `38.6%` win, `+13.4%` ROI, `1.34` A/E;
- agreement >= 2: `33.3%` win, `+10.2%` ROI, `1.32` A/E.

These are **historical results, not forward-test results and not guarantees**. They motivate the frozen model; they do not count toward the public forward ledger.

## 11. Supersession rule

This Canon model supersedes the older coefficient sets for Race 001 onward. Historical results from older generations remain historical and must stay labeled with their original generation.

Any change to the formula, required features, regime definitions, Conviction equation, absolute bands, or longshot boundary after registration requires a new methodology version and new preregistration. Existing records never move to the new model retroactively.
