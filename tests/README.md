# tests — refusal-first

The suite is written the way the environment behaves: the
refusals are tested before the passes. **89 tests**, run from
the repository root with `pytest`.

- `test_gates.py`, `test_sellers.py` — the gates and Gate 0:
  drift, mislabelling, short history, over-cap, unmeasured —
  each refused by name.
- `test_delivery.py`, `test_sam.py`, `test_sam_mask.py` —
  the delivery gate and the SAM mask decoding (the mask test
  runs offline on the recorded payload in `fixtures/`).
- `test_receipts.py` — the chain: tamper breaks replay;
  replay reproduces a run bit-for-bit.
- `test_brain.py`, `test_probes.py` — the liveliness
  profile and the probe battery, including the probe whose
  failure is a finding, not a bug: refusal recall.
- `test_run.py`, `test_tenant.py`, `test_parse.py`,
  `test_demo.py`, `test_refuse_api.py` — the run loop, the
  tenant's replaceability, mandate parsing, the demo, and
  the public refuse path.
