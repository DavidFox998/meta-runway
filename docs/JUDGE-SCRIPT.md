# The two-minute judge script — Runway

*For a reviewer with ten minutes and a terminal. Everything on the
no-key path runs offline against recorded runs; the live path at the
end needs a Meta Model API key. Expected outputs are quoted from runs
verified on 2026-11-01 against main at the Gate 0 merge.*

The claim being demonstrated: an AI agent (Muse Spark) placed inside
a runtime environment — a mandate she cannot edit, gates that
re-measure every claim, money that moves only on a pass, and a
receipt chain anyone can replay. The demo's three beats are the
product's three sentences: **a claim is measured, a tamper is refused
by name, a clean run settles — and all of it replays.**

## 0:00–0:20 — the suite (refusal-first)

```bash
git clone https://github.com/DavidFox998/soph-e-runway && cd soph-e-runway
python -m pytest -q
```

Expected: **89 passed.** The suite is written refusal-first: gates
are tested on what they refuse (over-cap, attribute mismatch, seller
drift, insufficient history, tampered receipts) before what they
pass.

## 0:20–0:50 — the demo (watch it refuse, then settle)

```bash
python demo/serve.py   # then open http://127.0.0.1:8791/
```

The page runs the environment live against its recorded merchant
choreography: a claim is asserted (3850¢), the gates measure it, a
tampered delivery is **refused by name** (`attribute_mismatch:
colour`), the seller with a drifting record is refused too
(`seller_price_drift`), and the recovery run **settles 3499¢**. The
receipt chain grows in the corner as it happens — every verdict an
entry, every entry naming the hash of the one before it.

## 0:50–1:20 — replay a recorded live run (the receipt is the proof)

No key, no trust required — the recorded chains verify themselves:

```bash
PYTHONPATH=src python - <<'EOF'
from runway.receipts import ReceiptChain
for name in ("receipt_settle", "receipt_refuse"):
    c = ReceiptChain.from_jsonl(
        open(f"artifacts/live_run_20261027T192237Z/{name}.jsonl").read())
    print(name, len(c.entries), "entries, verify:", c.verify())
    c.replay()  # re-derives the run; raises on any mismatch
EOF
```

Expected: both chains print **verify: True** (7 and 5 entries), and
the replay completes without a mismatch. Change one byte in a copy
of either file and `verify()` returns False — the tamper tests in
`tests/test_receipts.py` do exactly this.

## 1:20–2:00 — Gate 0, and the two honest misses

```bash
python scripts/gate0_evaluate.py
```

Expected: **archetype separation: 4/4** — the honest seller passes;
the drifter, the mislabeler, and the newcomer are each refused, by
name (`seller_price_drift`, `seller_attribute_mismatch`,
`insufficient_history`). Gate 0 judges the claimant, not the claim:
a seller's own record can refuse it before its offer is measured.

Then read `docs/gate4-confusion-matrix.md`: Gate 4 (SAM 3.1,
mask-measured) judged **18 of 20** delivery photographs correctly,
and the two misses are published in the same document that reports
the eighteen — a true kettle refused on a tight spout close-up
(`item_absent`), a blurred photograph passed though too weak to
trust. The misses are part of the demo, not a footnote to it.

## Optional — the live path (Meta Model API key required)

```bash
python scripts/live_run.py
```

Runs Muse Spark live through the settle and refuse scenarios and
writes a new recorded run under `artifacts/live_run_<timestamp>/`,
with receipt heads and a replay check in its `summary.json`. This is
the run the film's numbers come from.

*Motto: measured, not minted — proven, not asserted.*
