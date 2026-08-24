# Settlement Records

Official post-race settlements live here. The frozen public settlement schema is [`schema-v1.json`](./schema-v1.json).

A settlement references the immutable pre-race `record_id` and appends outcome information without altering the original prediction.

## Required behavior

- use the official result source;
- preserve the official result source URL and a source-artifact hash when available;
- retain field-wide final odds/probabilities when they can be reconstructed consistently, so market-relative grading can be reproduced;
- settle the headline record at the official pari-mutuel WIN payoff;
- keep PASS/EXCLUDED races as `no_bet` rather than deleting them;
- mark scratches/cancellations explicitly;
- never replace an official final payoff with the more favorable decision-time price.

## One-unit settlement convention

For a normal U.S. `$2` official win payoff `P`:

```text
units_returned = P / 2
pnl_units      = units_returned - 1
```

A losing 1-unit BET returns `0` and has `pnl_units = -1`.

A PASS/EXCLUDED race has `stake_units = 0`, `units_returned = 0`, and `pnl_units = 0`.

Scratches/cancellations are void under the registered rules and do not manufacture a win or loss.

## Grading fields

For a settled runner outcome `y` in `{0,1}`:

```text
brier_contrib        = (model_prob - y)^2
market_brier_contrib = (market_prob_decision - y)^2
```

Log loss is computed with probabilities clipped only by the frozen reporting implementation to prevent `log(0)`; the clipping constant must be declared before the first aggregate report.

Where official final field odds are available and de-vigged consistently:

```text
mbm_prob_gap = model_prob - market_prob_final
```

This is the pari-mutuel market-relative measure; it is not classic fixed-price CLV.

## Immutability

Settlement files are append-only evidence. If a later official correction changes the result, preserve the original settlement and add a new dated correction record referencing it rather than silently rewriting the historical commit.
