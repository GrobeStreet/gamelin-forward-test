# GAMELIN Canon v1.0 — Forward-Test Data Input Protocol

**Status: PARTIALLY FROZEN — CURRENT PP INPUT RIGHTS/COVERAGE BLOCKER — RACE 001 LOCKED**

This document freezes the intended race-state and market-timing protocol for the first public Del Mar forward test and identifies the one remaining unresolved input dependency: a rights-cleared, complete source of current ClassRating and prior SpeedFigure inputs matching the Canon feature definitions.

## 1. Circuit and race identity

Initial circuit: **Del Mar Thoroughbred Club (DMR)**.

Primary official race-card source:

`https://www.dmtc.com/racing/entries`

For each race, the pre-race record must preserve:

- race date;
- race number;
- official/track race identity where available;
- surface;
- distance;
- race class/conditions;
- purse;
- scheduled/estimated post time displayed by the official card;
- active program numbers and runner names after known scratches.

A copy/hash of the card state used for the decision must be retained as an audit artifact when the capture implementation is completed.

## 2. Scratches and official changes

Primary official change source:

`https://www.dmtc.com/racing/changes`

The Del Mar page identifies these as official changes and states that they are updated several times per hour.

Before the decision odds are frozen, the current changes page must be checked and all scratches known at that time applied to the active field. The record must preserve:

- changes source URL;
- observation timestamp UTC;
- source-posted update time when present;
- scratched program numbers/names;
- surface/rail/track-condition changes relevant to race identity/state.

A runner scratched before decision time is not part of the probability normalization. A scratch announced after the locked decision is handled under the registered settlement/void rules and remains visible in the audit trail.

## 3. Decision-odds source

Primary official market display selected for the Del Mar test:

`https://www.dmtc.com/handicapping/odds`

The official Del Mar Live Odds page exposes, during live racing:

- race number;
- race date;
- minutes to post (`MTP`) / OFF state;
- program number;
- horse name;
- current odds.

The Del Mar mobile-app documentation also describes its Cybertote feature as providing Live Odds, Probables, Will-Pays, and Payouts.

This is selected over an automated Equibase-page scraping path because the forward test should use the track's own official live market presentation and avoid implying that public Equibase pages grant automated/commercial data rights.

## 4. Decision clock — frozen target

**Target decision state: the first complete official Del Mar odds snapshot observed while the Live Odds page displays `5 MTP`.**

A complete snapshot means every active runner has a valid displayed win price and the runner list matches the post-scratch field.

The lock procedure must record:

```text
source_observed_at_utc
source_mtp
source_url
runner_program_no
runner_name
observed_odds
```

The pre-race record must be committed immediately after the snapshot and strictly before the official off time.

### No discretionary waiting

Once a complete `5 MTP` snapshot has been observed, a later price may not replace it because it looks more favorable.

If a valid 5-MTP snapshot is not captured under the implementation's fixed observation procedure, the race is **EXCLUDED** from the registered headline ledger rather than backfilled with a later attractive price.

### Implementation proof still required

Before registration, the exact capture mechanism must be demonstrated to:

- observe the official page reproducibly;
- timestamp the capture;
- preserve a raw or hashed audit artifact;
- avoid operator choice among multiple snapshots;
- operate within the source's permitted access terms.

Until that implementation proof exists, the decision-source checklist in the preregistration remains open.

## 5. Market probability

For active runners at the locked decision snapshot:

```text
decimal_odds_i     = decimal representation of displayed win odds
raw_implied_prob_i = 1 / decimal_odds_i
market_prob_i      = raw_implied_prob_i / sum_j(raw_implied_prob_j)
```

The normalization is performed only after scratches known at the snapshot are removed.

Store both the displayed odds and derived probabilities. Never overwrite the observed price with the final tote price.

## 6. Required ClassRating input — BLOCKER

Canon v1.0 was fitted using the pre-race class-rating family documented in the 2023 Equibase PP research (`TodaysHorseClassRating` / PP `ClassRating`).

The forward test therefore requires a **current, rights-cleared source** that provides the same defined input for every active runner.

Current state:

- historical research access is documented;
- current production contains public-PP discovery/enrichment logic;
- that is not sufficient evidence that GAMELIN has stable rights and complete race-by-race coverage for a public automated forward-test feed;
- public Equibase product pages describe Class Ratings and Speed Figures as PP/product data, which reinforces that access/usage terms must be respected.

**Race 001 cannot start until this source is resolved.**

## 7. Required recent-SpeedFigure input — BLOCKER

Canon v1.0 defines `recent_speed` as the average of the runner's last three prior pre-race Speed Figures from the same feature family used in model validation.

The registered source must provide sufficient prior-start history to compute the feature for every active runner without using post-race information from the race being predicted.

Required frozen transform:

```text
recent_speed = arithmetic mean(last 3 available prior SpeedFigure values)
```

The exact missing-history rule must be fixed before registration. For v1.0, the preferred conservative rule is **exclude the race if any active runner lacks the required three prior values**, unless the historical model's parser is reproduced and demonstrates a different pre-existing missing-value rule.

No substitute speed scale may be silently mapped into this feature after registration.

## 8. Identity reconciliation

Before scoring:

- program number and normalized runner name must match across card, change, odds, and PP input sources;
- duplicate or ambiguous matches invalidate the race;
- scratches must reconcile to the active field;
- all source observations must be pre-race.

Any unresolved identity conflict is an `EXCLUDED` race with a reason code, not a manual guess.

## 9. Data-rights rule

The forward test will not treat historical research access as commercial redistribution permission.

The public evidence repo should expose GAMELIN-derived probabilities, action states, timestamps, and enough observed market information to audit the decision. It should not republish full proprietary PP files or a raw commercial data feed.

A future enterprise integration should prefer customer-supplied or contractually licensed underlying race data.

## 10. Current gate state

Frozen:

- Del Mar initial circuit;
- official Del Mar race-card source;
- official Del Mar changes source;
- official Del Mar Live Odds page as intended decision-market source;
- 5-MTP target state;
- de-vigging calculation;
- strict identity reconciliation;
- full-model-only headline test.

Still blocking registration:

1. rights-cleared, complete current source for Canon ClassRating;
2. rights-cleared, complete current source for last-three SpeedFigure history;
3. reproducible 5-MTP capture implementation and access-term verification;
4. exact missing-history behavior matched to the validated model.

**Race 001 remains locked.**
