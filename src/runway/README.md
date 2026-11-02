# src/runway — the environment

Module map, in the order a purchase meets them:

- `parse.py` — the mandate, parsed into exact, checkable
  terms. Ambiguity refuses here.
- `tenant.py` — the proposer (Muse Spark). Replaceable by
  design: the environment holds the line, not the tenant.
- `client.py` — the Meta Model API client (Standard tier
  only; contributor-tier models are refused in code).
- `claims.py` — typed claims: assertion and measurement in
  different fields.
- `gates.py` — the mandate, offer and payment gates, and the
  `Verdict` type every gate returns.
- `sellers.py` — Gate 0: the seller's own record, measured
  before its first offer is.
- `sam.py` — the SAM 3.1 client.
- `delivery.py` — Gate 4: the delivery photo measured from
  the mask's own pixels.
- `ledger.py` — assets under seal: movement only on a pass,
  exactly once, within the cap.
- `receipts.py` — the hash-chained receipt chain and its
  replay.
- `brain.py`, `probes.py` — the heartbeat over the tenant
  itself: cognitive probes, and the liveliness profile they
  produce (measured, never asserted).
- `run.py` — the environment: the run loop that wires
  tenant, gates, ledger and chain together.
- `demo_run.py`, `demo_feed.py` — the demo cabinet's run
  and its live feed.

Trap: a verdict is never the tenant's. Anything the tenant
asserts arrives as a claim and leaves as a measurement, a
pass, or a refusal with its reason named.
