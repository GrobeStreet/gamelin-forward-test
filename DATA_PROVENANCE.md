# GAMELIN Data Provenance

Status: **P0 canonicalization record — public corpus wording reconciled**

This file records the research datasets documented in the GAMELIN evidence base and separates source-level counts from marketing aggregates.

## U.S. — Equibase 2023 results

- 318,702 starter rows
- 42,618 races
- 126 U.S. tracks
- Full calendar year: 2023-01-01 through 2023-12-31
- 84,627 distinct horses
- 4,764 trainers
- 1,547 jockeys

Documented contents include result charts, fractions, calls, beaten lengths, payoffs, odds, race types, class, post, connections, and other result-chart fields.

## U.S. — Equibase 2023 Past Performances

- 5,930 daily race cards
- approximately 1.8 GB
- approximately 94% join rate to results

Documented feature families include Class Ratings, Speed Figures, and Pace Figures. These data were used in the U.S. win-picker / Conviction research.

**Accounting rule:** PP-card rows are not added to the public starter-record subtotal below because they are another representation of runners already represented in the U.S. results universe and because the current evidence ledger does not expose a clean non-overlap row count for the joined PP table.

## U.S. — NYRA GPS tracking

- 5,228,430 GPS pings
- 14,915 horse-race observations
- 1,944 races
- Aqueduct, Belmont, Saratoga

Documented use: per-stride/position research and testing of pace-related hypotheses.

**Accounting rule:** GPS pings are reported separately, not added to starter-record totals.

## UK / Ireland

- 1,253,081 runner rows
- 125,473 races
- 2016–2026

Documented use: Official Rating research and multi-year validation of the OR-stack signal.

## Multinational historical archive

- 4,107,315 runner rows
- 396,572 races
- 442 courses
- 1990–2020

Documented use: long-horizon robustness work and leakage detection, including identification of post-race leakage in RPR/TR-derived fields.

## Hong Kong sectional / live-odds research

- 79,447 runner rows in the documented sectional/runs set
- 6,348 races with sectional split data
- 260,042 live-odds snapshots
- 1,519 races with live-odds history
- median approximately 171 snapshots per race in the evidence ledger

Documented use: sectional-pace research and odds-movement / drift analysis.

## Canonical public starter-record subtotal

The four primary runner/starter row counts that are explicitly itemized are:

```text
Equibase U.S. 2023          318,702
UK / Ireland              1,253,081
Multinational archive     4,107,315
Hong Kong sectional runs     79,447
                          ---------
Subtotal                  5,758,545
```

This subtotal is mechanically reproducible from the documented source-level counts.

### Approved public wording

> **"GAMELIN's research program processed 5.7M+ starter-level records across multiple racing datasets, including the complete 2023 Equibase U.S. results season."**

Important: `5,758,545` is a **record-count subtotal across datasets**, not a claim of 5,758,545 unique horses or non-overlapping real-world race participations. Some source families can cover overlapping jurisdictions/time periods.

## Reconciliation of the historical `6.0M` / `6,003,247` claim

The evidence ledger separately states approximately **6.0 million runners** and an exact aggregate of `6,003,247`.

P0 cannot reproduce `6,003,247` from the currently exposed itemized primary runner counts without adding approximately `244,702` records from secondary/supplementary representations. The available ledger text does not identify a clean non-overlap manifest that explains that difference.

Therefore:

- `6,003,247` remains a **historical evidence-ledger aggregate**;
- it is not approved as the default public corpus count for Canon v1.0;
- it may be restored only if a file-level manifest reproduces the total and defines its overlap/accounting rules.

## Reconciliation of the historical `612K races` claim

The evidence ledger also states approximately `612,000` races. The currently itemized primary race counts do not mechanically reproduce that total, and some datasets may overlap by jurisdiction/time period.

Therefore:

- source-specific race counts are approved;
- the aggregate `~612K races` claim is **not approved as a Canon v1.0 headline** until a race-level manifest/accounting rule reproduces it.

## Reconciliation of the historical `8M+` claim

Older artifacts used `8M+` wording. No source manifest currently available in P0 substantiates `8M+` as a clean canonical starter-record total.

Disposition: **deprecated / not approved for public Canon v1.0 claims.**

## Other approved scale facts

These are source-specific and should not be added into the 5.7M starter subtotal as if they were comparable row types:

- 5.23 million NYRA GPS pings processed;
- 260,042 live-odds snapshots in the documented HK/SG odds research;
- 40+ predictive signals/hypotheses tested, per the evidence ledger;
- U.S. 2023: 318,702 starters / 42,618 races / 126 tracks.

## Data-rights boundary

Historical access and research use do not automatically establish commercial redistribution rights.

P0 therefore distinguishes three concepts:

1. **Research provenance** — what data supported historical experiments.
2. **Forward-test input rights** — what data may lawfully be used to generate the public test record.
3. **Enterprise commercialization rights** — what data may be consumed, retained, derived from, exposed, or sublicensed in a paid product.

The preferred first enterprise architecture is customer-supplied or otherwise rights-cleared race/tote data feeding GAMELIN-derived analytics.

## Prohibited provenance behavior

- Do not describe scraped or manually observed ADW data as a licensed production feed.
- Do not publish proprietary raw PP fields merely because they were available for research.
- Do not merge post-race information into pre-race features.
- Do not present record counts as unique horses/races unless deduplication has actually been performed.
- Do not silently revise dataset totals after publication; changes require a dated update with explanation.
