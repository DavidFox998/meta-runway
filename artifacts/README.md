# artifacts — recorded runs, kept whole

Nothing here is regenerated or edited after the fact; a run's
directory is its record.

Each `live_run_*` directory holds one live run of the
environment with the hosted Muse Spark tenant:

- `profile.json` — the liveliness profile: probe beats,
  coherence, continuity, calibration error, response median.
- `receipt_settle.jsonl` / `receipt_refuse.jsonl` — the
  hash-chained receipts for the run's scenarios. They replay
  bit-for-bit; the demo branch's `/verify` endpoint replays
  every recorded chain in the browser.
- `summary.json`, `transcript.txt` — the run's summary and
  full transcript.

The profile the submission cites is
`live_run_20261027T192237Z` (after the probe-context fix:
coherence 6/7, calibration error 0.186).

Also here: `probe_A_*.json` and `probe_B_*.json` (the first
brain probes, 2026-10-27), `gate0_evaluation.json` (the
Gate 0 seller-separation result, reproduced by
`scripts/gate0_evaluate.py`), and the two `seller_battery_*`
runs (Gate 0's battery against the hosted and open models).

Trap: the open-weights comparison battery's artifacts live on
the branch `live/spark-open-battery`, not here — including
the disclosure that its run 1 lost its profile to a bug in
our runner (see that branch's `docs/spark-open-comparison.md`).
