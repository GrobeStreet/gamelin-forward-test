# GAMELIN Claims Register

Status: **P0 canonicalization record — Canon v1.0 model claims reconciled**

This register separates descriptive product claims, historical/backtest claims, and future forward-test claims. Quantitative claims may not silently migrate between categories.

## A. Approved descriptive claims

These may be used now, with ordinary context:

- GAMELIN is a horse-racing decision/intelligence engine, not a wagering operator.
- GAMELIN separates projected winner from whether the current price justifies a primary wager.
- GAMELIN can return PASS / `$0` rather than forcing action.
- GAMELIN's research program used walk-forward evaluation and actively tested for leakage.
- GAMELIN documented negative findings instead of retaining every intuitive handicapping factor.
- `GAMELIN-CANON-v1.0` uses market, class, recent speed, signal agreement, race-regime terms, and a separate Conviction Index.
- The model's projected winner and its highest-Conviction betting candidate may be different horses.
- Probability edge and monetary expected value are different quantities in Canon v1.0.

## B. Approved corpus wording

The mechanically reproducible primary runner/starter subtotal is `5,758,545` records across the itemized Equibase U.S., UK/IRE, multinational archive, and Hong Kong runner datasets.

Approved public headline:

> **"GAMELIN's research program processed 5.7M+ starter-level records across multiple racing datasets, including the complete 2023 Equibase U.S. results season."**

Required interpretation:

- this is a record count across datasets, not a unique-horse count;
- overlapping jurisdictions/time periods may exist across source families;
- GPS pings and odds snapshots are separate data types and are not added into this subtotal.

Also approved as source-specific scale facts:

- U.S. Equibase 2023: `318,702` starters / `42,618` races / `126` tracks;
- NYRA GPS: approximately `5.23M` pings;
- HK/SG odds research: `260,042` odds snapshots;
- `40+` hypotheses/signals tested, per the evidence ledger.

## C. Canon-v1 historical validation claims — BACKTEST ONLY

The June 2 final-engine sync explicitly attaches the following historical results to the final Conviction generation that became `GAMELIN-CANON-v1.0`:

| Claim | Historical result | Status |
|---|---:|---|
| Full validated sample | 6,559 races | BACKTEST / source-labeled |
| Strict date holdout, top-conviction pick | 31.1% win; +5.7% ROI | BACKTEST |
| Market comparator in same holdout | -3.9% ROI | BACKTEST |
| Bootstrap | median ~+6%; 98% positive resamples | BACKTEST |
| All top-conviction picks | 30.8% win; +4.5% ROI; 1.26 A/E | BACKTEST |
| Conviction top-50% | 35.5% win; +10.6% ROI; 1.33 A/E | BACKTEST |
| Conviction top-25% | 39.3% win; +13.1% ROI; 1.36 A/E | BACKTEST |
| Conviction top-10% | 41.6% win; +13.7% ROI; 1.36 A/E | BACKTEST |
| Agreement = 3 | 38.6% win; +13.4% ROI; 1.34 A/E | BACKTEST |
| Agreement >= 2 | 33.3% win; +10.2% ROI; 1.32 A/E | BACKTEST |

Required qualifier when any ROI number is used:

> **Historical backtest / walk-forward result from the pre-forward-test research record. It is not a live profitability guarantee and does not count toward the public forward ledger.**

No claim above may be relabeled as forward performance.

## D. Historical claims from superseded generations

The following may remain in research history but are not Canon-v1 performance claims unless explicitly labeled with their original generation:

- 31.4% top-pick accuracy from the earlier three-factor winner model;
- older allowance/stakes/small-field hit-rate claims tied to Generation A/B gates;
- any historical result generated under the `2.20/.36/.45` or `1.738/.387/.585` coefficient sets.

## E. Separate non-U.S. research claims

The UK/IRE Official Rating stack and Hong Kong sectional/drift findings are separate research modules. They are not evidence that the Canon v1.0 U.S. forward-test engine is profitable.

If cited, jurisdiction, sample period, model/signal, and BACKTEST status must be explicit.

## F. Deprecated / unresolved claims

Do not use as Canon v1.0 headlines:

- `6,003,247 runners` / `6.0M runners` as a canonical aggregate unless a file-level accounting manifest reproduces the total and explains overlaps;
- `~612K races` as a canonical aggregate unless a race-level accounting manifest reproduces it;
- `8M+ runners`;
- any statement implying that historical U.S. backtest ROI is established live profitability;
- any claim that an older coefficient set's performance automatically transfers to Canon v1.0.

## G. Forbidden claims

- guaranteed winner / lock / certainty language;
- guaranteed profit or guaranteed positive ROI;
- "GAMELIN beats the market" as a live/current claim before the registered forward record supports it;
- cherry-picked winner screenshots presented as representative performance;
- unqualified claims of superior pace, trainer/jockey hot-angle, post-position, or other signals that the research ledger reports as dead ends;
- performance claims based on post-race leakage fields;
- calling `model_prob - market_prob` monetary expected value.

## H. Forward-test claim rule

After Race 001, every quantitative live claim must point to the append-only forward ledger and be labeled **FORWARD TEST**.

The public hierarchy will be:

1. calibration / Brier skill vs. the registered market baseline;
2. Model-Beat-Market probability comparison;
3. flat-stake ROI with sample size and bootstrap confidence interval;
4. drawdown / losing-streak / BET-rate / PASS-rate context.

Historical BACKTEST and live FORWARD TEST numbers are never blended into one performance statistic.
