# GAMELIN — Limited Data Request for Del Mar Forward Test

## Purpose

GAMELIN is preparing a preregistered, public, append-only forward evaluation of a horse-racing probability/decision model. The initial test is deliberately narrow: **Del Mar Thoroughbred Club, U.S. pari-mutuel WIN decisions, one primary BET or PASS per eligible race.**

Historical model development used the complimentary 2023 Equibase research dataset. Before beginning live forward testing, GAMELIN is seeking a rights-cleared path for the current proprietary feature families required by the frozen model.

## Requested current inputs

For each active runner on supported Del Mar cards:

1. **Today's Horse Class Rating / ClassRating**
2. **Prior Equibase Speed Figures** sufficient to compute:

```text
recent_speed = average of last 3 prior SpeedFigure values
```

Race identity/program number/horse name are required only to reconcile the features to the official field.

## What GAMELIN would publish

The public evidence repository is designed to expose derivative model/evaluation outputs, not reproduce a PP product.

Examples:

- model win probability;
- de-vigged market probability;
- probability edge;
- Conviction score/band;
- BET / PASS;
- model version + methodology hash;
- timestamps;
- result/settlement and calibration metrics.

The public ledger can store derived within-field percentiles and hashes of the feature-input artifact rather than raw proprietary ClassRating/SpeedFigure values.

## What GAMELIN would not publish

- full PP files;
- a raw ClassRating or SpeedFigure feed;
- downloadable historical Equibase/TrackMaster datasets;
- source credentials/tokens;
- source data sold or sublicensed as a substitute for Equibase/TrackMaster products.

## Requested rights / pilot terms

For the first phase, GAMELIN is asking whether Equibase / TrackMaster / TJC Innovations can provide either written permission or a limited data arrangement covering:

- Del Mar only;
- current pre-race research/evaluation use;
- feature retention long enough to audit the registered test;
- publication of GAMELIN-derived outputs as described above;
- internal/model-input use of the ClassRating and prior SpeedFigure fields;
- no raw-data redistribution.

## Evidence protocol

Before Race 001:

- model and gate are frozen;
- methodology is hashed;
- all eligible races are logged before post;
- PASS decisions and losses remain public;
- official settlement is appended after the race;
- no historical result counts toward the forward test.

The first formal readout is preregistered for the later of **200 settled qualifying BETs or 60 calendar days**.

## Longer-term architecture

If the forward test is useful, the preferred enterprise design is:

```text
licensed/customer-supplied racing data
          -> GAMELIN inference
          -> derivative probability / conviction / action output
```

GAMELIN does not need to become a redistributor of the underlying racing database.
