# GAMELIN Claims Register

Status: **P0 canonicalization working record**

No statement below becomes a Canon v1.0 public performance claim until its source, model generation, and wording are reconciled.

## Provisionally approved descriptive claims

These describe the research/product process rather than promising live profitability.

- GAMELIN is a horse-racing decision/intelligence engine, not a wagering operator.
- GAMELIN separates projected winner from whether the current price justifies a wager.
- GAMELIN can return PASS / $0 rather than forcing action.
- GAMELIN's research program used walk-forward evaluation and actively tested for leakage.
- GAMELIN documented negative findings instead of retaining every intuitive handicapping factor.
- The current production candidate combines market, class, speed, agreement, and race-regime information and also computes a Conviction Index.
- The research ledger documents approximately 6.0M runners and approximately 612K races across multiple jurisdictions, subject to final corpus reconciliation.

## Historical quantitative claims requiring model-generation labels

These may be true for specific historical experiments but **must not be presented as current Canon performance without reconciliation**.

- top pick approximately 30–31% overall in certain U.S. fitted/walk-forward experiments;
- approximately 35–39% top-pick hit rates in certain race-type/field-size subsets;
- Conviction-selected subsets showing positive historical ROI in specific backtests;
- consensus pattern results involving market/class/speed agreement;
- UK/IRE Official Rating stack historical ROI claims;
- any +ROI, A/E, bootstrap, or favorite-comparison figure from historical analyses.

Each surviving claim must eventually include:

```text
claim_id
exact wording
model generation
sample
period
market/jurisdiction
metric definition
source artifact
known limitations
status
```

## Deprecated / unresolved claims

Do not use publicly until P0 resolves them:

- "5.7M+ starter-level records"
- "6M+ runners" without the reconciliation footnote
- "8M+ runners"
- any statement implying that historical U.S. backtest ROI is established live profitability
- any claim that the newest production model automatically inherits performance measured under an older coefficient set

## Forbidden claims

- guaranteed winner / lock / certainty language
- guaranteed profit or guaranteed positive ROI
- "GAMELIN beats the market" without a registered forward result that supports that statement
- cherry-picked winner screenshots presented as representative performance
- unqualified claims of superior pace, trainer/jockey hot-angle, post-position, or other signals that the research ledger reports as dead ends
- performance claims based on post-race leakage fields

## Canon wording rule

After P0, every quantitative public claim must point to either:

1. a frozen historical result explicitly labeled **BACKTEST**, or
2. the append-only forward record explicitly labeled **FORWARD TEST**.

Those categories are never blended.
