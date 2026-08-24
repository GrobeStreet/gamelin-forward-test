# Forward-Test Ledger

Status: **NOT ACTIVE — Race 001 locked pending Canon v1.0 registration.**

Each eligible race will receive a pre-race record committed before post.

Minimum record fields:

```text
record_id
race_id
track
race_date
race_number
post_time
logged_at_utc
source_event_time
model_version
methodology_hash
race_state_hash
runner_id
runner_name
model_probability
market_probability
decision_odds
edge
expected_value
conviction
decision
reason_codes
```

Rules:

- prediction blocks are immutable after commit;
- PASS decisions remain in the ledger;
- exclusions/missed races are explicitly logged;
- official results are appended in `settlements/`, never written back into the prediction block.
