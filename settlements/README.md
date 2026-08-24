# Settlement Records

Official post-race settlements live here.

A settlement references the immutable pre-race `record_id` and appends outcome information without altering the original prediction.

Minimum settlement fields:

```text
record_id
race_id
official_result_source
settled_at_utc
runner_id
finish_position
win_payoff
status
units_staked
units_returned
net_units
notes
```

Valid `status` values should include at least `settled`, `void_scratch`, `void_cancelled`, and `dead_heat` as applicable.
