# GAMELIN Data Provenance

Status: **P0 canonicalization working record**

This file records the research datasets currently documented in the GAMELIN evidence base. Counts are source-derived and remain subject to reconciliation for overlap, deduplication, and public-claim wording.

## U.S. — Equibase 2023 results

- 318,702 starters
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

## U.S. — NYRA GPS tracking

- 5,228,430 GPS pings
- 14,915 horse-race observations
- 1,944 races
- Aqueduct, Belmont, Saratoga

Documented use: per-stride/position research and testing of pace-related hypotheses.

## UK / Ireland

- 1,253,081 runners
- 125,473 races
- 2016–2026

Documented use: Official Rating research and multi-year validation of the OR-stack signal.

## Multinational historical archive

- 4,107,315 runners
- 396,572 races
- 442 courses
- 1990–2020

Documented use: long-horizon robustness work and leakage detection, including identification of post-race leakage in RPR/TR-derived fields.

## Hong Kong

- 79,447 runners
- 6,348 races with sectional split data
- 260,042 live-odds snapshots
- 1,519 races with live-odds history
- median approximately 171 snapshots per race in the documented ledger

Documented use: sectional-pace research and odds-movement / drift analysis.

## Headline corpus accounting

The current evidence ledger states:

- approximately **6.0 million runners** analyzed (6,003,247 across listed datasets)
- approximately **612,000 races**
- 5+ jurisdictions/countries
- 1990–2026 span
- 5.23 million GPS pings
- 260,042 live tote/odds snapshots
- 40+ hypotheses/signals tested

### Important reconciliation note

Other GAMELIN artifacts have used **5.7M+** or **8M+** wording. Those figures are **not approved as canonical claims yet**. P0 must determine whether those numbers reflect:

- different snapshot dates;
- starter-level vs runner-level counting;
- inclusion of overlapping datasets;
- additional files not represented in the evidence ledger;
- or simple stale marketing copy.

Until reconciled, the detailed evidence-ledger counts above are the working source of truth.

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
- Do not silently revise dataset totals after publication; changes require a dated update with explanation.
