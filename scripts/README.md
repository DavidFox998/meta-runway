# scripts — the runnable entry points

- `live_run.py` — a live run of the environment with the
  hosted Muse Spark tenant: works the mandate's scenarios
  through every gate and writes the run's directory under
  `artifacts/`. Spends real Meta Model API credits.
- `gate0_evaluate.py` — reproduces the Gate 0 seller
  separation over the recorded seller records and writes
  `artifacts/gate0_evaluation.json`. Offline; no credits.
- `probe_sam.py` — the SAM 3.1 probe: segments a photo
  (`assets/probe_kettle.jpg` by default) and reports the
  mask measurements the delivery gate consumes.
