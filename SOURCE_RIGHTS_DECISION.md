# GAMELIN P0 — Source Rights Decision

**Status: DECIDED — DO NOT SCRAPE EQUIBASE / TRACKMASTER PP DATA FOR RACE 001**

## Decision

The first registered forward test will not automate access to current Equibase/TrackMaster PP pages or republish their raw ClassRating/SpeedFigure fields without written permission or a contractually permitted data path.

This is now a P0 rule, not a suggestion.

## Why

Canon v1.0 needs the same feature families used in its validated U.S. research:

- `TodaysHorseClassRating` / ClassRating;
- prior Equibase SpeedFigure history sufficient to compute `recent_speed`.

Current Equibase product pages state that their site Terms of Use prohibit robots/spiders/scrapers/other automated access and prohibit republication or dissemination without prior written consent. Equibase registration terms also describe acquired information as personal-use data and require written permission before dissemination to a third party.

TrackMaster's current public product pages identify Equibase Speed Figures and Equibase Class Ratings as proprietary/value-added data products and provide a business-development contact for data inquiries.

Therefore a 'free scraper' is not an acceptable evidence foundation for this repository.

## Chosen path

Request a **narrow research/pilot permission or data arrangement** for the Del Mar forward test.

Minimum requested scope:

- Del Mar only to start;
- current-day pre-race ClassRating for active runners;
- enough prior SpeedFigure history to compute last-three recent speed;
- research/evaluation use in a preregistered public forward test;
- permission to publish **derived GAMELIN outputs only**, not raw PP files or raw proprietary rating feeds;
- retention of hashes/provenance needed for audit;
- no wagering execution or resale of the underlying data.

The preferred commercial architecture remains the same later: customer-supplied or licensed race data in, GAMELIN-derived probabilities/decision outputs out.

## Why a purchased consumer PP alone does not clear P0

A consumer PP card may solve technical availability, but the currently located Equibase registration terms describe acquired information as for personal use and restrict dissemination without written permission. Because the forward-test repository is public and intended as a commercial credibility asset, P0 will not assume that a normal consumer purchase silently grants the required public/derived-output rights.

## Contact route

Current official TrackMaster directory lists:

- **Jim Vanderbosch — Vice President, Business Development**
- `jim@trackmaster.com`
- TrackMaster / Equibase, 821 Corporate Drive, Lexington, KY

Equibase's 2024 research-dataset announcement also identifies Jim Vanderbosch as vice president for sales and business development and explicitly frames the complimentary dataset as an on-ramp for product development/innovation.

TJC Innovations has publicly stated that it serves customers seeking larger datasets for AI/ML and has supplied North American Thoroughbred data to AI companies.

## Race 001 consequence

**Race 001 stays locked until we have a rights-cleared current ClassRating/SpeedFigure path.**

If permission is denied or economically impractical, the scientifically honest alternatives are:

1. create a separately fitted model using legally available features and register that as a future Canon version; or
2. run a market-only public test as a distinct model/ledger, not pretend it is Canon v1.0.

We will not change the current Canon inputs simply to make Race 001 easier to start.
