# Forward-Test Ledger

Status: **NOT ACTIVE — Race 001 locked pending final Canon v1.0 registration.**

The public pre-race schema is frozen in [`schema-v1.json`](./schema-v1.json).

## Unit of record

One immutable JSON file per race, containing:

- race identity/state;
- exact observation/generation timestamps;
- source URLs and source-artifact hashes;
- model version and methodology hash;
- the full active field's derived Canon inputs and probabilities;
- projected winner;
- highest-Conviction candidate;
- primary `BET`, `PASS`, or `EXCLUDED` decision;
- reason codes;
- integrity hashes.

The ledger stores **derived feature percentiles**, not raw proprietary PP ClassRating/SpeedFigure values. A hash of the underlying feature-input artifact can be preserved for audit without republishing the raw source product.

## Naming convention

Planned path:

```text
ledger/YYYY-MM-DD/DMR-RNN-<record_id>.json
```

The exact file is committed before official off time. Its pre-race contents are never updated after the race.

## Decision-state semantics

- `BET` — exactly 1.00 flat unit on the registered selected runner.
- `PASS` — race was valid and scored, but the registered wager gate failed; stake 0.
- `EXCLUDED` — race failed the registered data/identity/timing eligibility rules; stake 0.

PASS and EXCLUDED races remain part of the coverage record.

## Probability semantics

```text
edge_pp     = model_prob - market_prob
ev_decision = model_prob * decision_odds_decimal - 1
```

`edge_pp` is not monetary EV.

## Immutability rule

- pre-race record is committed before off;
- settlement never edits the pre-race file;
- post-race data goes into `settlements/` referencing the same `record_id`;
- if an error is discovered later, preserve the original file and add a dated correction/audit note rather than rewriting history.
